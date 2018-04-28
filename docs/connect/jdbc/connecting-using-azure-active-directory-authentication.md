---
title: Conectar-se usando a autenticação do Active Directory do Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.technology:
- drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ef69bb70de8af6b6dc56df66e652f7f4dae7529c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectar-se usando a autenticação do Active Directory do Azure

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre como desenvolver aplicativos do Java para usar o recurso de autenticação do Active Directory do Azure com o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server.

Você pode usar a autenticação do Azure AAD (Active Directory), que é um mecanismo de se conectar ao banco de dados SQL v12 usando identidades do Active Directory do Azure. Use a autenticação do Active Directory do Azure para gerenciar centralmente as identidades de usuários de banco de dados e como uma alternativa para autenticação do SQL Server. O Driver JDBC permite que você especifique suas credenciais do Active Directory do Azure na cadeia de caracteres de conexão JDBC para se conectar ao banco de dados de SQL do Azure. Para obter informações sobre como configurar a autenticação do Active Directory do Azure, visite [se conectar ao SQL banco de dados, usando o Azure Active Directory Authentication](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Duas novas propriedades de conexão foram adicionadas para dar suporte a autenticação do Active Directory do Azure:
*   **autenticação**: Use essa propriedade para indicar qual método de autenticação de SQL a ser usado para conexão. Os valores possíveis são: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword**e o padrão **NotSpecified**.
    * Use ' autenticação = ActiveDirectoryIntegrated' para se conectar ao banco de dados SQL usando a autenticação integrada do Windows. Para usar esse modo de autenticação, você precisa federar o local federação serviços ADFS (Active Directory) com o AD do Azure na nuvem. Depois que isso é configurado, bem como um tíquete Kerberos, você pode acessar o banco de dados do Azure SQL sem precisar inserir as credenciais quando você estiver conectado em um computador ingressado no domínio. 
    * Use ' autenticação = ActiveDirectoryPassword' para se conectar ao banco de dados SQL usando um nome principal do AD do Azure e a senha.
    * Use ' autenticação = SqlPassword' para se conectar a um SQL Server usando as propriedades de nome de usuário e senha.
    * Use ' autenticação = NotSpecified' ou deixá-lo como padrão quando nenhum desses métodos de autenticação são necessários.

*   **accessToken**: Use essa propriedade para se conectar a um banco de dados SQL usando um token de acesso. accessToken só pode ser definida usando o parâmetro de propriedades do método getConnection() na classe do Gerenciador de driver. Ele não pode ser usado na URL de conexão.  

Para obter detalhes, consulte a propriedade de autenticação no [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) página.  


## <a name="client-setup-requirements"></a>Requisitos de instalação do cliente
Certifique-se de que os seguintes componentes são instalados no computador cliente:
* Java 7 ou superior
*   Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server
*   Se você estiver usando o modo de autenticação baseada em token de acesso, você precisa [do azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências para executar os exemplos neste artigo. Para obter mais informações, consulte **conectando-se com um Token de acesso** seção.
*   Se você estiver usando o modo de autenticação ActiveDirectoryPassword, será necessário [do azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências. Para obter mais informações, consulte **se conectar usando o modo de autenticação ActiveDirectoryPassword** seção.
*   Se você estiver usando o modo de ActiveDirectoryIntegrated, você precisa do azure Active Directory library para java e suas dependências. Para obter mais informações, consulte **se conectar usando o modo de autenticação ActiveDirectoryIntegrated** seção.
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conectar-se usando o modo de autenticação ActiveDirectoryIntegrated
 Com a versão 6.4, Microsoft JDBC Driver adiciona suporte para autenticação de ActiveDirectoryIntegrated usando um tíquete Kerberos em várias plataformas (Windows/Linux e Mac).
Consulte [tíquete Kerberos definida no Windows, Mac e do Linux](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) para obter mais detalhes. Como alternativa, no Windows, sqljdbc_auth.dll também pode ser usado para autenticação ActiveDirectoryIntegrated com o Driver JDBC.

> [!NOTE]
>  Se você estiver usando uma versão mais antiga do driver, verifique isso [link](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) para as respectivas dependências que são necessárias para usar esse modo de autenticação. 

O exemplo a seguir mostra como usar ' autenticação = ActiveDirectoryIntegrated' modo. Execute esse exemplo em um computador ingressado no domínio federado com o Active Directory do Azure. Um usuário de banco de dados independente que representa a entidade de segurança do AD do Azure, ou um dos grupos, pertence a, deve existir no banco de dados e deve ter a permissão CONNECT. 

Antes de criar e executar o exemplo, no computador cliente (em que, para executar o exemplo a), baixe o [biblioteca azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e incluí-los no caminho de compilação de Java

Substitua o nome de servidor/banco de dados com o nome de servidor/banco de dados nas seguintes linhas antes de executar o exemplo:

```
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

O exemplo para usar o modo de autenticação ActiveDirectoryIntegrated:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class IntegratedExample {

    public static void main(String[] args) throws Exception {
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
Executar este exemplo em um computador cliente automaticamente usa o tíquete Kerberos e nenhuma senha é necessária. Se uma conexão for estabelecida, você verá a seguinte mensagem:
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Definir o tíquete do Kerberos no Windows, Mac e do Linux

Você precisa configurar um tíquete Kerberos vinculando o usuário atual para uma conta de domínio do Windows. Um resumo das etapas principais está incluído abaixo.

#### <a name="windows"></a>Windows
Acompanha o JDK `kinit` que você pode usar para obter um TGT do KDC (Key Distribution Center) em um domínio Unido máquina é federada com o Active Directory do Azure.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Etapa 1: Recuperação de tíquete de concessão de tíquete
- **Executar em**: Windows
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC, em seguida, ele solicitará sua senha de domínio.
  - Use `klist` para ver as permissões disponíveis. Se o kinit foi bem-sucedida, você verá um tíquete de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Talvez seja necessário especificar um `.ini` arquivo com `-Djava.security.krb5.conf` para seu aplicativo localizar o KDC.

#### <a name="linux-and-mac"></a>Linux e Mac

##### <a name="requirements"></a>Requisitos
Acesso a um computador ingressado no domínio do Windows para consultar seu controlador de domínio do Kerberos

##### <a name="step-1-find-kerberos-kdc"></a>Etapa 1: Localizar o KDC do Kerberos
- **Executar em**: linha de comando do Windows
- **Ação**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (onde "DOMAIN.COMPANY.COM" mapeia para o nome do domínio)
- **Saída de exemplo**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Informações para extrair** nomear o controlador de domínio, nesse caso `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Etapa 2: Configurando o KDC no krb5
- **Executar em**: Linux/Mac
- **Ação**: editar o /etc/krb5.conf em um editor de sua escolha. Configurar as chaves a seguir
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Em seguida, salve o arquivo krb5 conf e sair

> [!NOTE]
>  Domínio deve ser todo em maiusculas.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Etapa 3: Testando a recuperação de tíquete de concessão de tíquete
- **Executar em**: Linux/Mac
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC, em seguida, ele solicitará sua senha de domínio.
  - Use `klist` para ver as permissões disponíveis. Se o kinit foi bem-sucedida, você verá um tíquete de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Conectar-se usando o modo de autenticação ActiveDirectoryPassword
O exemplo a seguir mostra como usar ' autenticação = ActiveDirectoryPassword' modo.

Antes de criar e executar o exemplo:
1.  No computador cliente (em que, para executar o exemplo a), baixe o [biblioteca azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e incluí-los no caminho de compilação de Java
2.  Localize as seguintes linhas de código e substitua o nome de servidor/banco de dados pelo nome do servidor/banco de dados.
    ```
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Localize as seguintes linhas de código e substitua o nome de usuário, com o nome do usuário do AD do Azure que você deseja se conectar como.
    ```
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

O exemplo para usar o modo de autenticação ActiveDirectoryPassword:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class UserPasswordExample {
    
    public static void main(String[] args) throws Exception{
        SQLServerDataSource ds = new SQLServerDataSource();
        
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        Connection connection = ds.getConnection();
        
        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
Se a conexão é estabelecida, você verá a seguinte mensagem de saída:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Deve existir um banco de dados de usuário independente e um usuário de banco de dados independente que representa o usuário do AD do Azure ou um dos grupos, o Azure especificado pertence ao usuário do AD, deve existir no banco de dados e deve ter a permissão CONNECT (com exceção do Active Directory do Azure administrador do servidor ou grupo)


## <a name="connecting-using-access-token"></a>Conectando-se com um Token de acesso
Aplicativos/serviços pode recuperar um token de acesso do Active Directory do Azure e usá-lo para se conectar ao banco de dados do SQL Azure. Observe que accessToken só pode ser definida usando o parâmetro de propriedades do método getConnection() na classe do Gerenciador de driver. Ele não pode ser usado na cadeia de conexão.
 
O exemplo a seguir contém um simple aplicativo Java que se conecta ao banco de dados do SQL Azure usando a autenticação baseada em token de acesso. Antes de criar e executar o exemplo, execute as seguintes etapas:
1.  Crie uma conta do aplicativo no Azure Active Directory para o serviço.
    1. Entrar no portal de gerenciamento do Azure
    2. Clique no Active Directory do Azure, no painel de navegação à esquerda
    3. Clique na guia "Registros do aplicativo".
    4. Na gaveta, clique em "Novo application registration".
    5. Digite mytokentest como um nome amigável para o aplicativo, selecione "aplicativo/API da Web".
    6. Não é preciso URL de logon. Basta fornecer qualquer coisa: "http://mytokentest".
    7. Clique em "Criar" na parte inferior.
    9. Ainda no portal do Azure, clique na guia "Configurações" do seu aplicativo e abra a guia "Propriedades".
    10. Localize o valor de "ID do aplicativo" (também conhecido como ID do cliente) e copie-o à parte, você precisará isso mais tarde ao configurar seu aplicativo (por exemplo, 1846943b-ad04-4808-aa13-4702d908b5c1). Consulte o instantâneo a seguir.
    11. Localize o valor "URL de ID do aplicativo" e copie-o à parte, esta é a URL de STS.
    12. Na seção "Chaves", crie uma chave preenchendo o campo de nome, selecionando a duração da chave, e salvar a configuração (deixe o campo de valor vazio). Depois de salvar, o campo de valor deve ser preenchido automaticamente, copie o valor gerado. Esse é o segredo do cliente.

    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Faça logon no banco de dados de usuário do servidor do SQL Azure como um administrador do Active Directory do Azure e usando um usuário de banco de dados independente de uma cláusula de comando T-SQL para seu aplicativo principal. Consulte o [se conectar ao banco de dados SQL ou SQL Data Warehouse por usando o Azure Active Directory Authentication](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) para obter mais detalhes sobre como criar um administrador do Active Directory do Azure e um usuário de banco de dados independente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  No computador cliente (em que, para executar o exemplo a), baixe o [azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) biblioteca e suas dependências e incluí-los no caminho de compilação de Java. Observe que o azure Active Directory-biblioteca-para-java só é necessário para executar esse exemplo específico, pois ele usa as APIs desta biblioteca para recuperar o token de acesso do AD do Azure. Se você já tiver um token de acesso, você pode ignorar esta etapa. Observe que você também precisará remover a seção de exemplo que recupera o token de acesso.

No exemplo a seguir, substitua o nome do URL do STS, ID do cliente, segredo do cliente, servidor e banco de dados com seus valores.

```
import java.sql.Connection;
import java.sql.ResultSet;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD. 
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;


public class TokenBasedExample {

    public static void main(String[] args) throws Exception{

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://microsoft.onmicrosoft.com/..."; // Replace with your STS URL.
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
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
``` 

Se a conexão for bem-sucedida, você verá a seguinte mensagem de saída:
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
