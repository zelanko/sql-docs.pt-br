---
title: Conectando-se usando a autenticação do Azure Active Directory
description: Saiba mais sobre como desenvolver aplicativos Java que usam o recurso de autenticação do Azure Active Directory com o Microsoft JDBC Driver for SQL Server.
ms.custom: ''
ms.date: 01/29/2020
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73b377076dfea329ba82c0219c28bf9c955d7e7f
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634812"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectando-se usando a autenticação do Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre como desenvolver aplicativos Java que usam o recurso de autenticação do Azure Active Directory com o Microsoft JDBC Driver for SQL Server.

É possível usar a Autenticação do AAD (Azure Active Directory), que é um mecanismo de conexão com o Banco de Dados SQL do Azure v12, que usa identidades no Azure Active Directory. Use a autenticação do Azure Active Directory para gerenciar centralmente as identidades de usuários do banco de dados e como uma alternativa à autenticação do SQL Server. O JDBC Driver permite que você especifique suas credenciais do Azure Active Directory na cadeia de conexão JDBC para se conectar ao BD SQL do Azure. Para obter informações sobre como configurar a autenticação do Azure Active Directory, acesse [Como conectar-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

As propriedades de conexão para dar suporte à Autenticação do Azure Active Directory no Microsoft JDBC Driver para SQL Server são:
*   **authentication**:  use essa propriedade para indicar qual método de autenticação SQL usar para a conexão. Os valores possíveis são: 
    * **ActiveDirectoryMSI**
        * Compatível desde a versão do driver **v7.2**, o `authentication=ActiveDirectoryMSI` pode ser usado para se conectar a um Banco de Dados SQL/SQL Data Warehouse do Azure de dentro de um recurso do Azure com suporte de "Identidade" habilitado. Opcionalmente, **msiClientId** também pode ser especificado nas propriedades Connection/DataSource junto com esse modo de autenticação, que deve conter a ID do cliente de uma Identidade de Serviço Gerenciada a ser usada para adquirir o **accessToken** para estabelecer a conexão.
    * **ActiveDirectoryIntegrated**
        * Compatível desde a versão do driver **v6.0**, o `authentication=ActiveDirectoryIntegrated` pode ser usado para se conectar a um Banco de Dados SQL/SQL Data Warehouse do Azure usando a autenticação integrada. Para usar esse modo de autenticação, você precisa federar o ADFS (Serviços de Federação do Active Directory) local com o Azure Active Directory na nuvem. Depois de configurado, você pode se conectar adicionando a biblioteca nativa 'mssql-jdbc_auth-\<versão>-\<arch>.dll' ao caminho da classe de aplicativo no sistema operacional Windows ou configurar um tíquete Kerberos para suporte de autenticação multiplataforma. Você poderá acessar o BD SQL do Azure/DW sem ser solicitado a fornecer credenciais quando estiver conectado a um computador ingressado no domínio.
    * **ActiveDirectoryPassword**
        * Compatível desde a versão do driver **v6.0**, o `authentication=ActiveDirectoryPassword` pode ser usado para se conectar a um Banco de Dados SQL/SQL Data Warehouse do Azure usando um nome e uma senha de entidade de segurança do Azure AD.
    * **SqlPassword**
        * Use `authentication=SqlPassword` para se conectar a um SQL Server usando as propriedades userName/user e password.
    * **NotSpecified**
        * Use `authentication=NotSpecified` ou deixe-o como o padrão quando nenhum desses métodos de autenticação for necessário.

*   **accessToken**: Use essa propriedade de conexão para se conectar a um Banco de Dados SQL usando um token de acesso. accessToken só pode ser definido usando o parâmetro Properties do método getConnection() na classe DriverManager. Ele não pode ser usado na URL de conexão.  

Para obter mais informações, confira a propriedade de autenticação na página [Configuração das propriedades de conexão](setting-the-connection-properties.md).  


## <a name="client-setup-requirements"></a>Requisitos de configuração do cliente
Para autenticação **ActiveDirectoryMSI**, os componentes abaixo devem ser instalados no computador cliente:
* Java 8 ou superior
* Microsoft JDBC Driver 7.2 (ou superior) para SQL Server
* O ambiente do cliente deve ser um recurso do Azure e deve ter o suporte ao recurso "Identidade" habilitado.
* Um usuário de banco de dados independente que representa a identidade gerenciada atribuída ao sistema do recurso do Azure ou a identidade gerenciada atribuída ao usuário ou um dos grupos aos quais seu MSI pertence, deve existir no banco de dados de destino e deve ter a permissão CONNECT.

Para outros modos de autenticação, os componentes abaixo devem ser instalados no computador cliente:
* Java 7 ou superior
* Microsoft JDBC Driver 6.0 (ou superior) para SQL Server
* Se estiver usando o modo de autenticação baseado em token de acesso, você precisará de [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e de suas dependências para executar os exemplos deste artigo. Para obter mais informações, confira a seção **Como conectar-se usando o token de acesso**.
* Se você estiver usando o modo de autenticação do **ActiveDirectoryPassword**, precisará do [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e de suas dependências. Para obter mais informações, confira a seção **Como conectar-se usando o modo de autenticação do ActiveDirectoryPassword**.
* Se estiver usando o modo do **ActiveDirectoryIntegrated**, você precisará do azure-activedirectory-library-for-java e de suas dependências. Para obter mais informações, confira a seção **Como conectar-se usando o modo de autenticação do ActiveDirectoryIntegrated**.

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>Como conectar-se usando o modo de autenticação do ActiveDirectoryMSI
O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryMSI`. Execute este exemplo de dentro de um recurso do Azure, por exemplo, uma Máquina Virtual do Azure, um Serviço de Aplicativo ou um Aplicativo de Funções federado com o Azure Active Directory.

Substitua o nome do servidor/banco de dados pelo nome do servidor/banco de dados nas seguintes linhas antes de executar o exemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

O exemplo para usar o modo de autenticação do ActiveDirectoryMSI:

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

A execução deste exemplo em uma Máquina Virtual do Azure busca um token de acesso de _identidade gerenciada atribuída ao sistema_ ou _identidade gerenciada atribuída ao usuário_ (se **msiClientId** está especificado) e estabelece uma conexão usando o token de acesso obtido. Se uma conexão for estabelecida, você deverá ver a seguinte mensagem:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Como conectar-se usando o modo de autenticação do ActiveDirectoryIntegrated
Com a versão 6.4, o Microsoft JDBC Driver adiciona suporte para autenticação ActiveDirectoryIntegrated usando um tíquete Kerberos em várias plataformas (Windows, Linux e macOS).
Para obter mais informações, confira [Definir tíquete Kerberos no Windows, Linux e macOS](#set-kerberos-ticket-on-windows-linux-and-macos). Como alternativa, no Windows, 'mssql-jdbc_auth-\<versão>-\<arch>.dll' também pode ser usada para autenticação ActiveDirectoryIntegrated com o JDBC Driver.

> [!NOTE]
>  Se você estiver usando uma versão mais antiga do driver, marque este [link](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) para as respectivas dependências que serão necessárias para usar esse modo de autenticação. 

O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryIntegrated`. Execute este exemplo em um computador ingressado no domínio que seja federado com o Azure Active Directory. Um usuário de banco de dados independente representando sua entidade de segurança do Azure AD ou um dos grupos aos quais você pertence deve existir no banco de dados e deve ter a permissão CONNECT. 

Antes de compilar e executar o exemplo, no computador cliente (no qual você deseja executar o exemplo), baixe a biblioteca [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e as inclua no caminho de build do Java

Substitua o nome do servidor/banco de dados pelo nome do servidor/banco de dados nas seguintes linhas antes de executar o exemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

O exemplo para usar o modo de autenticação do ActiveDirectoryIntegrated:
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

### <a name="set-kerberos-ticket-on-windows-linux-and-macos"></a>Definir tíquete Kerberos no Windows, Linux e macOS

Você precisa configurar um tíquete Kerberos vinculando o usuário atual a uma conta de domínio do Windows. Um resumo das principais etapas está incluído abaixo.

#### <a name="windows"></a>Windows
O JDK vem com o `kinit`, que você pode usar para obter um TGT do KDC (centro de distribuição de chaves) em um computador ingressado no domínio que seja federado com o Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Etapa 1: recuperação do tíquete de concessão de tíquete
- **Executar em**: Windows
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC e, em seguida, ele solicitará sua senha de domínio.
  - Use `klist` para ver os tíquetes disponíveis. Se o kinit tiver sido bem-sucedido, você verá um tíquete de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Talvez seja necessário especificar um arquivo `.ini` com `-Djava.security.krb5.conf` para que seu aplicativo localize o KDC.

#### <a name="linux-and-macos"></a>Linux e macOS

##### <a name="requirements"></a>Requisitos
Acesso a um computador ingressado no domínio do Windows para consultar o controlador de domínio do Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Etapa 1: localizar o KDC do Kerberos
- **Executar em**: Linha de comando do Windows
- **Ação**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (em que "DOMAIN.COMPANY.COM" é mapeado para o nome do seu domínio)
- **Saída de exemplo**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Informações para extrair** O nome do DC, neste caso, `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Etapa 2: configuração do KDC em krb5.conf
- **Executar em**: Linux/macOS
- **Ação**: editar o /etc/krb5.conf em um editor de sua escolha. Configure as seguintes chaves
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
- **Executar em**: Linux/macOS
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC e, em seguida, ele solicitará sua senha de domínio.
  - Use `klist` para ver os tíquetes disponíveis. Se o kinit tiver sido bem-sucedido, você verá um tíquete de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Como conectar-se usando o modo de autenticação do ActiveDirectoryPassword
O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryPassword`.

Antes de compilar e executar o exemplo:
1.  No computador cliente (no qual você deseja executar o exemplo), baixe a biblioteca [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e as inclua no caminho de build do Java
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

O exemplo para usar o modo de autenticação do ActiveDirectoryPassword:
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
Se uma conexão for estabelecida, você deverá ver a seguinte mensagem como resultado:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Um banco de dados de usuário independente deve existir e um usuário de banco de dados independente que representa o usuário do Azure AD especificado ou um dos grupos ou o usuário do Azure AD especificado ao qual ele pertence, deve existir no banco de dados e deve ter a permissão CONNECT (exceto para o administrador ou grupo do servidor do Azure Active Directory)

## <a name="connecting-using-access-token"></a>Como conectar-se usando um token de acesso
Os aplicativos/serviços podem recuperar um token de acesso do Azure Active Directory e usá-lo para se conectar ao Banco de Dados SQL/SQL Data Warehouse do Azure.

> [!NOTE] 
> **accessToken** só pode ser definido usando o parâmetro Properties do método getConnection() na classe DriverManager. Ele não pode ser usado na cadeia de conexão.

O exemplo a seguir contém um aplicativo Java simples que se conecta ao Banco de Dados SQL/SQL Data Warehouse do Azure usando a autenticação baseada em token de acesso. Antes de compilar e executar o exemplo, execute as seguintes etapas:
1.  Crie uma conta de aplicativo no Azure Active Directory para seu serviço.
    1. Entre no portal do Azure.
    2. No painel de navegação à esquerda, clique em Azure Active Directory.
    3. Clique na guia "Registros de aplicativo".
    4. Na gaveta, clique em "Novo registro de aplicativo".
    5. Insira mytokentest como um nome amigável para o aplicativo, selecione "Aplicativo Web/API".
    6. Não precisamos da URL DE LOGON. Basta fornecer qualquer coisa: "https://mytokentest".
    7. Clique em "Criar" na parte inferior.
    9. Ainda no portal do Azure, clique na guia "Configurações" do seu aplicativo e abra a guia "Propriedades".
    10. Localize o valor "ID do aplicativo" (também conhecido como ID do cliente) e copie-o para algum local; você precisará dele mais tarde ao configurar seu aplicativo (por exemplo, 1846943b-ad04-4808-aa13-4702d908b5c1). Veja o instantâneo a seguir.
    11. Na seção "Chaves", crie uma chave preenchendo o campo de nome, selecionando a duração da chave e salvando a configuração (deixe o campo de valor vazio). Depois de salvar, o campo de valor deve ser preenchido automaticamente. Copie o valor gerado. Esse é o Segredo do cliente.
    12. Clique em Azure Active Directory no painel à esquerda. Em "Registros de aplicativo", localize a guia "Pontos de extremidade". Copie a URL em "PONTO DE EXTREMIDADE DO TOKEN 2.0 DO OATH", que é a URL do STS.
    
    ![JDBC_AAD_Token](media/jdbc_aad_token.png)  
2. Entre no banco de dados de usuário do Azure SQL Server como um administrador do Azure Active Directory e, usando um comando T-SQL, provisione um usuário de banco de dados independente para a entidade de segurança do aplicativo. Para obter mais informações, confira [Como conectar-se ao Banco de Dados SQL ou ao SQL Data Warehouse usando a autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) para mais detalhes sobre como criar um administrador de Azure Active Directory e um usuário de banco de dados independente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  No computador cliente (no qual você deseja executar o exemplo), baixe a biblioteca [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e as inclua no caminho de build do Java. Observe que a azure-activedirectory-library-for-java é necessária apenas para executar esse exemplo específico. O exemplo usa as APIs desta biblioteca para recuperar o token de acesso do Azure AAD. Se você já tiver um token de acesso, ignore esta etapa. Observe que você também precisa remover a seção no exemplo que recupera o token de acesso.

No exemplo a seguir, substitua a URL do STS, a ID do cliente, o segredo do cliente, o servidor e o nome do banco de dados pelos seus valores.

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

Se a conexão for bem-sucedida, você verá uma mensagem semelhante à seguinte:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
