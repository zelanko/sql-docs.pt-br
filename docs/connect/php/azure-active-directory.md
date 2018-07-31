---
title: O Azure Active Directory | Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: 71e6b3b4556621b6bc8a8a4c7996cfdb47a12849
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979438"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Conectar usando a Autenticação do Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[O Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) é uma tecnologia de gerenciamento de ID de usuário central que opera como uma alternativa ao [autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). O Azure AD permite conexões com o banco de dados SQL do Microsoft Azure e SQL Data Warehouse com identidades federadas no Azure AD usando um nome de usuário e senha, autenticação integrada do Windows ou um token de acesso do AD do Azure; os drivers PHP para SQL Server oferecem suporte parcial para esses recursos.

Para usar o Azure AD, use o **autenticação** palavra-chave. Os valores que **autenticação** pode levar diante são explicadas na tabela a seguir.

|Palavra-chave|Valores|Descrição|
|-|-|-|
|**Autenticação**|Não configurado (padrão)|Modo de autenticação determinado por outras palavras-chave. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Autenticar diretamente a uma instância do SQL Server (que pode ser uma instância do Azure) usando um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando o **UID** e **PWD** palavras-chave. |
||`ActiveDirectoryPassword`|Autenticar com uma identidade do Active Directory do Azure usando um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando o **UID** e **PWD** palavras-chave. |

O **autenticação** palavra-chave afeta as configurações de segurança de conexão. Se ele for definido na cadeia de conexão e, em seguida, por padrão o **Encrypt** palavra-chave é definido como true, para que o cliente solicita criptografia. Além disso, o certificado do servidor será validado, independentemente da configuração de criptografia, a menos que **TrustServerCertificate** é definido como true. Isso é diferenciado da antiga e menos segura, método de logon, em que o certificado do servidor não é validado, a menos que a criptografia é especificamente solicitada na cadeia de conexão.

Antes de usar o Azure AD com os drivers PHP para SQL Server no Windows, certifique-se de que você instalou o [assistente Microsoft Online Services entrar](https://www.microsoft.com/download/details.aspx?id=41950) (não é necessário para Linux e MacOS).

#### <a name="limitations"></a>Limitações

No Windows, o driver ODBC subjacente dá suporte a um valor mais para o **autenticação** palavra-chave **ActiveDirectoryIntegrated**, mas os drivers PHP não oferece suporte a esse valor em qualquer plataforma e, portanto, também Não há suporte para autenticação baseada em token do AD do Azure.

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
## <a name="see-also"></a>Consulte Também  
[Usando o Azure Active Directory com o Driver ODBC](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)
