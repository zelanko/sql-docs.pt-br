---
title: "Conectar-se usando a autenticação do Active Directory do Azure | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.technology: drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3dde204d199935b25f492ed23fadb3c2d4e70a99
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectar-se usando a autenticação do Active Directory do Azure
Este artigo fornece informações sobre como desenvolver aplicativos do Java para usar o recurso de autenticação do Active Directory do Azure com o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server.

Começando com o Microsoft JDBC Driver 6.0 para SQL Server, você pode usar a autenticação do Azure Active Direcoty (AAD) que é um mecanismo de se conectar ao banco de dados SQL v12 usando identidades do Active Directory do Azure. Use a autenticação do Active Directory do Azure para gerenciar centralmente as identidades de usuários de banco de dados e como uma alternativa para autenticação do SQL Server. O JDBC Driver 6.0 (ou superior) permite que você especifique suas credenciais do Active Directory do Azure na cadeia de caracteres de conexão JDBC para se conectar ao banco de dados de SQL do Azure. Para obter informações sobre como configurar a autenticação do Active Directory do Azure, visite [se conectar ao SQL banco de dados, usando o Azure Active Directory Authentication](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Duas novas propriedades de conexão foram adicionadas para dar suporte a autenticação do Active Directory do Azure:
*   **autenticação**: Use essa propriedade para indicar qual método de autenticação de SQL a ser usado para conexão. Os valores possíveis são: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword** e o padrão **NotSpecified** .
    * Use ' autenticação = ActiveDirectoryIntegrated' para se conectar ao banco de dados SQL usando a autenticação integrada do Windows. Para usar esse modo de autenticação que você precisa para federar o local federação serviços ADFS (Active Directory) com o AD do Azure na nuvem. Após a instalação, você pode acessar o banco de dados de SQL do Azure sem precisar inserir ceredentials quando você estiver conectado em um computador ingressado no domínio. 
    * Use ' autenticação = ActiveDirectoryPassword' para se conectar ao banco de dados SQL usando um nome principal do AD do Azure e a senha.
    * Use ' autenticação = SqlPassword' para se conectar a um SQL Server usando as propriedades de nome de usuário e senha.
    * Use ' autenticação = NotSpecified' ou deixá-lo como padrão se nenhum desses métodos de autenticação é necessária.

*   **accessToken**: Use essa propriedade para se conectar a um banco de dados SQL usando um token de acesso. accessToken só pode ser definida usando o parâmetro de propriedades do método getConnection() na classe do Gerenciador de driver. Ele não pode ser usado na URL de conexão.  

Para obter detalhes, consulte a propriedade de autenticação no [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) página.  


## <a name="client-setup-requirements"></a>Requisitos de instalação do cliente
Certifique-se de que os seguintes componentes são instalados no computador cliente:
* Java 7 ou superior
*   Microsoft JDBC Driver 6.2 (ou superior) para o SQL Server
*   Se você estiver usando o modo de autenticação baseada em token de acesso, será necessário [do azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências para executar os exemplos neste artigo. Consulte **conectando-se com um Token de acesso** seção para obter mais detalhes.
*   Se você estiver usando o modo de autenticação ActiveDirectoryPassword você precisará [do azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências. Consulte **se conectar usando o modo de autenticação ActiveDirectoryPassword** seção para obter mais detalhes.
*   Se você estiver usando o modo de ActiveDirectoryIntegrated, você precisará instalar a biblioteca de autenticação do Active Directory para o SQL Server (ADALSQL. DLL) e sqljdbc_auth.dll.
    * ADALSQL. DLL permite que aplicativos se autentiquem no Microsoft Azure SQL Database usando o Active Directory do Azure. Baixar a DLL do [biblioteca de autenticação do Microsoft Active Directory do Microsoft SQL Server](http://www.microsoft.com/en-us/download/details.aspx?id=48742)
    * Para ADALSQL. DLL duas binárias versões X86 e X64 estão disponíveis para download. Se a versão binária incorreta está instalada ou se a DLL está ausente, o driver irá gerar o seguinte erro: "não é possível carregar adalsql.dll (Authentication =...). Código de erro: 0x2. ". Nesse caso, baixe a versão correta do ADALSQL. DLL. 
    * sqljdbc_auth.dll está disponível no pacote de driver. Copie o arquivo sqljdbc_auth.dll para um diretório no caminho do sistema Windows no computador onde o driver JDBC está instalado. Como alternativa, você pode definir a propriedade do sistema java.libary.path para especificar o diretório de sqljdbc_auth.dll. 
    * Se estiver executando uma JVM de 64 bits em um processador x64, use o arquivo sqljdbc_auth.dll na pasta x64. 
    * Se você estiver executando uma Máquina Virtual Java (JVM) de 32 bits, use o arquivo sqljdbc_auth.dll na pasta x86, mesmo se o sistema operacional for a versão x64. 
    * Por exemplo, se você estiver usando o JVM de 32 bits e o driver JDBC está instalado no diretório padrão, você pode especificar o local da DLL usando o seguinte argumento de máquina virtual (VM) quando o aplicativo Java for iniciado:  
        ```
        -Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86
        ```
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conectar-se usando o modo de autenticação ActiveDirectoryIntegrated
O exemplo a seguir mostra como usar ' autenticação = ActiveDirectoryIntegrated' modo. Execute esse exemplo em um computador ingressado no domínio federado com o Active Directory do Azure. Um usuário de banco de dados independente que representa a entidade de segurança do AD do Azure, ou um dos grupos, pertence a, deve existir no banco de dados e deve ter a permissão CONNECT. 
    
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
Executar este exemplo em um computador ingressado em um domínio federado com o Active Directory do Azure usará automaticamente suas credenciais do Windows e nenhuma senha é necessária. Se a conexão é estabelecida, você verá a seguinte mensagem:
```
You have successfully logged on as: <your domain user name>
```

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
    3. Clique em locatário do diretório onde você deseja registrar o aplicativo de exemplo. Isso deve ser o mesmo diretório que está associado com seu banco de dados (o servidor que hospeda seu banco de dados).
    4. Clique na guia aplicativos.
    5. Na gaveta, clique em Adicionar.
    6. Clique em "Adicionar um aplicativo que minha organização esteja desenvolvendo".
    7. Digite mytokentest como um nome amigável para o aplicativo, selecione "Aplicativo Web e/ou API Web" e clique em Avançar.
    8. Supondo que este aplicativo é um serviço/daemon e não é um aplicativo da web, ele não tem uma entrada URL ou URI da ID do aplicativo. Para esses dois campos, digite http://mytokentest
    9. Ainda no portal do Azure, clique na guia Configurar do seu aplicativo
    10. Localize o valor da ID do cliente e copie-o à parte, você precisará dela posteriormente quando configurar seu aplicativo (ou seja,  a4bbfe26-dbaa-4fec-8ef5-223d229f647d). Consulte o instantâneo abaixo.
    11. Na seção "Chaves", selecione a duração da chave, salvar a configuração e copie a chave para uso posterior. Esse é o segredo do cliente.
    12. Na parte inferior, clique em "Exibir pontos de extremidade" e copie a URL em "ENDPOINT de autorização do OAUTH 2.0" para uso posterior. Esta é a URL do STS.


![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)


2. Faça logon para o banco de dados de usuário do servidor do SQL Azure como um administrador do Active Directory do Azure e usando um usuário de banco de dados independente de uma cláusula de comando T-SQL para a entidade de segurança do aplicativo. Consulte o [se conectar ao banco de dados SQL ou SQL Data Warehouse por usando o Azure Active Directory Authentication](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/) para obter mais detalhes sobre como criar um administrador do Active Directory do Azure e um usuário de banco de dados independente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  No computador cliente (em que, para executar o exemplo a), baixe o [azure Active Directory library para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) biblioteca e suas dependências e incluí-los no caminho de compilação de Java. Observe que o azure Active Directory-biblioteca-para-java só é necessário para executar esse exemplo específico, pois ele usa as APIs desta biblioteca para recuperar o token de acesso do AD do Azure. Se você já tiver um token de acesso, você pode ignorar esta etapa. Observe que você também precisará remover a seção de exemplo que recupera o token de acesso.

No exemplo a seguir, substitua a URL do STS, ID do cliente, segredo do cliente, servidor e nome de banco de dados com seus valores.

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
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "a4bbfe26-dbaa-4fec-8ef5-223d229f647d"; // Replace with your client ID.
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
