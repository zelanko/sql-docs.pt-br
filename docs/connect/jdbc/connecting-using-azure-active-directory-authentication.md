---
title: Conectando-se usando a autenticação do Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028117"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectando-se usando a autenticação do Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre como desenvolver aplicativos Java para usar o recurso de autenticação Azure Active Directory com o Microsoft JDBC Driver para SQL Server.

Você pode usar a autenticação do Azure Active Directory (AAD), que é um mecanismo de conexão ao banco de dados SQL do Azure V12 usando identidades no Azure Active Directory. Use a autenticação do Azure Active Directory para gerenciar centralmente as identidades de usuários do banco de dados e como uma alternativa à autenticação do SQL Server. O driver JDBC permite que você especifique suas credenciais de Azure Active Directory na cadeia de conexão JDBC para se conectar ao BD SQL do Azure. Para obter informações sobre como configurar a autenticação [de Azure Active Directory, visite conectar-se ao banco de dados SQL usando a autenticação Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

As propriedades de conexão para dar suporte à autenticação Azure Active Directory no Microsoft JDBC Driver para SQL Server são:
*   **autenticação**: Use essa propriedade para indicar qual método de autenticação SQL usar para a conexão. Os valores possíveis são: 
    * **ActiveDirectoryMSI**
        * Com suporte desde a versão do driver `authentication=ActiveDirectoryMSI` **v 7.2**, pode ser usado para se conectar a um banco de dados SQL do Azure/data warehouse de dentro de um recurso do Azure com suporte de "identidade" habilitado. Opcionalmente, **msiClientId** também pode ser especificado nas propriedades Connection/DataSource junto com esse modo de autenticação, que deve conter a ID do cliente de um identidade de serviço gerenciada a ser usado para adquirir o **accessToken** para estabelecer a conexão.
    * **ActiveDirectoryIntegrated**
        * Com suporte desde a versão do driver `authentication=ActiveDirectoryIntegrated` **v 6.0**, o pode ser usado para se conectar a um banco de dados SQL do Azure/data warehouse usando a autenticação integrada. Para usar esse modo de autenticação, você precisa federar o Serviços de Federação do Active Directory (AD FS) local (ADFS) com Azure Active Directory na nuvem. Depois de configurado, você pode se conectar adicionando a biblioteca nativa ' sqljdbc_auth. dll ' ao caminho da classe de aplicativo no sistema operacional Windows ou configurando um tíquete Kerberos para suporte de autenticação entre plataformas. Você poderá acessar o BD SQL do Azure/DW sem ser solicitado a fornecer credenciais quando estiver conectado a um computador ingressado no domínio.
    * **ActiveDirectoryPassword**
        * Com suporte desde a versão do driver `authentication=ActiveDirectoryPassword` **v 6.0**, o pode ser usado para se conectar a um banco de dados SQL do Azure/data warehouse usando um nome de entidade de segurança e senha do Azure AD.
    * **SqlPassword**
        * Use `authentication=SqlPassword` para se conectar a um SQL Server usando as propriedades de nome de usuário e senha.
    * **NotSpecified**
        * Use `authentication=NotSpecified` ou deixe como o padrão quando nenhum desses métodos de autenticação forem necessários.

*   **accessToken**: Use essa propriedade de conexão para se conectar a um banco de dados SQL usando um token de acesso. accessToken só pode ser definido usando o parâmetro Properties do método getConnection () na classe DriverManager. Ele não pode ser usado na URL de conexão.  

Para obter mais informações, consulte a propriedade de autenticação na página [definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md) .  


## <a name="client-setup-requirements"></a>Requisitos de instalação do cliente
Para a autenticação **ActiveDirectoryMSI** , os componentes a seguir devem ser instalados no computador cliente:
* Java 8 ou superior
* Microsoft JDBC Driver 7,2 (ou superior) para SQL Server
* O ambiente do cliente deve ser um recurso do Azure e deve ter o suporte ao recurso de "identidade" habilitado.
* Um usuário de banco de dados independente que representa a identidade gerenciada atribuída pelo sistema do recurso do Azure ou a identidade gerenciada atribuída pelo usuário ou um dos grupos aos quais seu MSI pertence, deve existir no banco de dados de destino e deve ter a permissão CONNECT.

Para outros modos de autenticação, os componentes a seguir devem ser instalados no computador cliente:
* Java 7 ou superior
* Microsoft JDBC Driver 6,0 (ou superior) para SQL Server
* Se você estiver usando o modo de autenticação baseada em token de acesso, precisará [do Azure-ActiveDirectory-library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e de suas dependências para executar os exemplos deste artigo. Para obter mais informações, consulte a seção **conectando usando o token de acesso** .
* Se você estiver usando o modo de autenticação **ActiveDirectoryPassword** , precisará [do Azure-ActiveDirectory-library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e de suas dependências. Para obter mais informações, consulte a seção **conectando usando o modo de autenticação ActiveDirectoryPassword** .
* Se você estiver usando o modo **ActiveDirectoryIntegrated** , precisará do Azure-ActiveDirectory-library-for-Java e de suas dependências. Para obter mais informações, consulte a seção **conectando usando o modo de autenticação ActiveDirectoryIntegrated** .

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>Conectando usando o modo de autenticação ActiveDirectoryMSI
O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryMSI`. Execute este exemplo de dentro de um recurso do Azure, e, g uma máquina virtual do Azure, serviço de aplicativo ou um Aplicativo de funções federado com Azure Active Directory.

Substitua o nome do servidor/banco de dados pelo nome do servidor/banco de dados nas seguintes linhas antes de executar o exemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

O exemplo para usar o modo de autenticação ActiveDirectoryMSI:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

A execução deste exemplo em uma máquina virtual do Azure busca um token de acesso da identidade gerenciada atribuída pelo _sistema_ ou da _identidade gerenciada atribuída pelo usuário_ (se **msiClientId** for especificado) e estabelece uma conexão usando o acesso Obtido token. Se uma conexão for estabelecida, você deverá ver a seguinte mensagem:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conectando usando o modo de autenticação ActiveDirectoryIntegrated
Com a versão 6,4, o Microsoft JDBC Driver adiciona suporte para autenticação ActiveDirectoryIntegrated usando um tíquete Kerberos em várias plataformas (Windows, Linux e macOS).
Para obter mais informações, consulte [set Kerberos ticket on Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) para obter mais detalhes. Como alternativa, no Windows, sqljdbc_auth. dll também pode ser usado para autenticação ActiveDirectoryIntegrated com o driver JDBC.

> [!NOTE]
>  Se você estiver usando uma versão mais antiga do driver, verifique este [link](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) para as respectivas dependências que são necessárias para usar esse modo de autenticação. 

O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryIntegrated`. Execute este exemplo em um computador ingressado no domínio que seja federado com Azure Active Directory. Um usuário de banco de dados independente representando sua entidade de segurança do Azure AD ou um dos grupos aos quais você pertence deve existir no banco de dados e deve ter a permissão CONNECT. 

Antes de compilar e executar o exemplo, no computador cliente (no qual você deseja executar o exemplo), baixe a [biblioteca Azure-ActiveDirectory-library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e as inclua no caminho de compilação do Java

Substitua o nome do servidor/banco de dados pelo nome do servidor/banco de dados nas seguintes linhas antes de executar o exemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

O exemplo para usar o modo de autenticação ActiveDirectoryIntegrated:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Executar este exemplo em um computador cliente usa automaticamente seu tíquete Kerberos e nenhuma senha é necessária. Se uma conexão for estabelecida, você deverá ver a seguinte mensagem:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Definir tíquete Kerberos no Windows, Linux e Mac

Você precisa configurar um tíquete Kerberos vinculando o usuário atual a uma conta de domínio do Windows. Um resumo das principais etapas está incluído abaixo.

#### <a name="windows"></a>Windows
O JDK é `kinit`fornecido com o, que pode ser usado para obter um TGT de centro de distribuição de chaves (KDC) em um computador ingressado no domínio que seja federado com Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Etapa 1: recuperação de tíquete de concessão de tíquete
- **Executar em**: Windows
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC e ele solicitará sua senha de domínio.
  - Use `klist` para ver os tíquetes disponíveis. Se o kinit tiver sido bem-sucedido, você deverá ver um tíquete de krbtgt/domínio. COMPANY. COM @ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Talvez seja necessário especificar um `.ini` arquivo com `-Djava.security.krb5.conf` o para que seu aplicativo localize o KDC.

#### <a name="linux-and-mac"></a>Linux e Mac

##### <a name="requirements"></a>Requisitos
Acesso a um computador ingressado no domínio do Windows para consultar o controlador de domínio do Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Etapa 1: localizar o KDC Kerberos
- **Executar em**: linha de comando do Windows
- **Ação**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (onde "Domain.Company.com" é mapeado para o nome do seu domínio)
- **Saída de exemplo**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Informações a serem extraídas** O nome do DC, neste caso`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Etapa 2: Configurando o KDC em krb5. conf
- **Executar em**: Linux/Mac
- **Ação**: Edite o/etc/krb5.conf em um editor de sua escolha. Configure as seguintes chaves
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Em seguida, salve o arquivo krb5.conf e saia

> [!NOTE]
>  O domínio precisa estar em MAIÚSCULAS.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Etapa 3: teste a recuperação do tíquete de concessão de tíquete
- **Executar em**: Linux/Mac
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC e ele solicitará sua senha de domínio.
  - Use `klist` para ver os tíquetes disponíveis. Se o kinit tiver sido bem-sucedido, você deverá ver um tíquete de krbtgt/domínio. COMPANY. COM @ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Conectando usando o modo de autenticação ActiveDirectoryPassword
O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryPassword`.

Antes de compilar e executar o exemplo:
1.  No computador cliente (no qual você deseja executar o exemplo), baixe a [biblioteca Azure-ActiveDirectory-library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e as inclua no caminho de compilação do Java
2.  Localize as linhas de código a seguir e substitua o nome do servidor/banco de dados pelo nome do servidor/banco de dados.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Localize as linhas de código a seguir e substitua o nome de usuário pelo nome do usuário do AAD ao qual você deseja se conectar.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

O exemplo para usar o modo de autenticação ActiveDirectoryPassword:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
Se a conexão for estabelecida, você deverá ver a seguinte mensagem como saída:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Um banco de dados de usuário independente deve existir e um usuário de banco de dados independente que representa o usuário do Azure AD especificado ou um dos grupos, o usuário do Azure AD especificado pertence, deve existir no banco de dados e deve ter a permissão CONNECT (exceto por Azure Active Directory administrador ou grupo do servidor)

## <a name="connecting-using-access-token"></a>Conectando usando o token de acesso
Aplicativos/serviços podem recuperar um token de acesso do Azure Active Directory e usá-lo para se conectar ao banco de dados SQL/data warehouse do Azure.

> [!NOTE] 
> **accessToken** só pode ser definido usando o parâmetro Properties do método getConnection () na classe DriverManager. Ele não pode ser usado na cadeia de conexão.

O exemplo a seguir contém um aplicativo Java simples que se conecta ao banco de dados SQL do Azure/data warehouse usando a autenticação baseada em token de acesso. Antes de compilar e executar o exemplo, execute as seguintes etapas:
1.  Crie uma conta de aplicativo no Azure Active Directory para seu serviço.
    1. Entre no portal do Azure.
    2. Clique em Azure Active Directory no painel de navegação à esquerda.
    3. Clique na guia "Registros de aplicativo".
    4. Na gaveta, clique em "novo registro de aplicativo".
    5. Insira mytokentest como um nome amigável para o aplicativo, selecione "aplicativo Web/API".
    6. Não precisamos de URL de logon. Basta fornecer algo: "https://mytokentest".
    7. Clique em "criar" na parte inferior.
    9. Ainda no portal do Azure, clique na guia "configurações" do seu aplicativo e abra a guia "Propriedades".
    10. Localize o valor "ID do aplicativo" (também conhecido como ID do cliente) e copie-o de lado, você precisará dele mais tarde ao configurar seu aplicativo (por exemplo, 1846943b-ad04-4808-aa13-4702d908b5c1). Consulte o instantâneo a seguir.
    11. Na seção "chaves", crie uma chave preenchendo o campo nome, selecionando a duração da chave e salvando a configuração (Deixe o campo valor vazio). Depois de salvar, o campo valor deve ser preenchido automaticamente, copie o valor gerado. Esse é o Segredo do cliente.
    12. Clique em Azure Active Directory no painel do lado esquerdo. Em "registros do aplicativo", localize a guia "pontos de extremidade". Copie a URL em "ponto de extremidade de TOKEN 2,0 OATH", que é a URL do STS.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Entre no banco de dados de usuário do Azure SQL Server como um administrador de Azure Active Directory e usando um comando T-SQL provisionar um usuário de banco de dados independente para a entidade de segurança do aplicativo. Para obter mais informações, consulte [conectando-se ao banco de dados SQL ou SQL data warehouse usando a autenticação Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) para obter mais detalhes sobre como criar um administrador de Azure Active Directory e um usuário de banco de dados independente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  No computador cliente (no qual você deseja executar o exemplo), baixe a biblioteca [Azure-ActiveDirectory-library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e inclua-as no caminho de compilação do Java. Observe que o Azure-ActiveDirectory-library-for-Java é necessário apenas para executar esse exemplo específico. O exemplo usa as APIs desta biblioteca para recuperar o token de acesso do Azure AAD. Se você já tiver um token de acesso, poderá ignorar esta etapa. Observe que você também precisa remover a seção no exemplo que recupera o token de acesso.

No exemplo a seguir, substitua a URL do STS, a ID do cliente, o segredo do cliente, o servidor e o nome do banco de dados pelos valores.

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

Se a conexão for bem-sucedida, você deverá ver a seguinte mensagem como saída:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
