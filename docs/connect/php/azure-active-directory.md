---
title: Active Directory do Azure | Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.suite: sql
ms.custom: 
ms.technology: drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.workload: Inactive
ms.openlocfilehash: eb13c1a57c63ce013a3b546572994106b8b1ffc0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="connect-using-azure-active-directory-authentication"></a>Conecte-se usando a autenticação do Active Directory do Azure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Active Directory do Azure](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) (AD do Azure) é uma tecnologia de gerenciamento de ID de usuário central que funciona como uma alternativa para [autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). O AD do Azure permite conexões ao banco de dados SQL do Microsoft Azure e SQL Data Warehouse com identidades federadas no AD do Azure usando um nome de usuário e senha, autenticação integrada do Windows ou um token de acesso do AD do Azure; os drivers PHP para SQL Server oferecem suporte parcial para esses recursos.

Para usar o AD do Azure, use o **autenticação** palavra-chave. Os valores que **autenticação** pode levar no são explicadas na tabela a seguir.

|Palavra-chave|Valores|Description|
|-|-|-|
|**Autenticação**|Não definido (padrão)|Modo de autenticação determinado por outras palavras-chave. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Autenticar diretamente a uma instância do SQL Server (que pode ser uma instância do Azure) usando um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando o **UID** e **PWD** palavras-chave. |
||`ActiveDirectoryPassword`|Autenticar com uma identidade do Active Directory do Azure usando um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando o **UID** e **PWD** palavras-chave. |

O **autenticação** palavra-chave afeta as configurações de segurança de conexão. Se estiver definido na cadeia de conexão e, em seguida, por padrão o **Encrypt** palavra-chave é definida como true, para que o cliente solicita criptografia. Além disso, o certificado do servidor será validado independentemente da configuração de criptografia, a menos que **TrustServerCertificate** é definido como true. Isso é distinto do antigo e menos segura, método de logon, em que o certificado do servidor não é validado, a menos que solicitado especificamente criptografia na cadeia de conexão.

Antes de usar o AD do Azure com os drivers PHP para SQL Server no Windows, certifique-se de que você tenha instalado o [assistente Microsoft Online Services entrar](https://www.microsoft.com/download/details.aspx?id=41950) (não é necessário para Linux e MacOS).

#### <a name="limitations"></a>Limitações

No Windows, o driver ODBC subjacente oferece suporte a um valor mais para o **autenticação** palavra-chave, **ActiveDirectoryIntegrated**, mas os drivers PHP não oferece suporte a esse valor em qualquer plataforma e, portanto, também não dão suporte a autenticação baseada em token do AD do Azure.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como se conectar usando **SqlPassword** e **ActiveDirectoryPassword**.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = array( "UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword' );

    $conn = sqlsrv_connect( $serverName, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=SqlPassword.\n";
        sqlsrv_close( $conn );
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = array( "Database"=>$azureDatabase, "UID"=>$azureUsername, "PWD"=>$azurePassword,
                             "Authentication"=>'ActiveDirectoryPassword' );

    $conn = sqlsrv_connect( $azureServer, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        sqlsrv_close( $conn );
    }

    ?>
```

O exemplo a seguir faz o mesmo que acima com o driver PDO_SQLSRV.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword );
        echo "Connected successfully with Authentication=SqlPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword );
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    ?>
```
## <a name="see-also"></a>Consulte também  
[Usando o Active Directory do Azure com o Driver ODBC](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory)
