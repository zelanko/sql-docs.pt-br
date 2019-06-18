---
title: O Azure Active Directory | Microsoft Docs
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: david-puglielli
ms.author: v-dapugl
manager: mbarwin
ms.openlocfilehash: 30423cd7c15a920d99fad4c0ea08e074beaece0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62522806"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Conectar usando a Autenticação do Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[O Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) é uma tecnologia de gerenciamento de ID de usuário central que opera como uma alternativa ao [autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD permite conexões ao banco de dados SQL do Microsoft Azure e SQL Data Warehouse com identidades federadas no Azure AD usando um nome de usuário e senha, autenticação integrada do Windows ou um token de acesso do AD do Azure. Os drivers PHP para SQL Server oferecem suporte parcial para esses recursos.

Para usar o Azure AD, use o **autenticação** ou **AccessToken** palavras-chave (elas são mutuamente exclusivas), conforme mostrado na tabela a seguir. Para obter mais detalhes técnicos, consulte [usando o Azure Active Directory com o Driver ODBC](../../connect/odbc/using-azure-active-directory.md).

|Palavra-chave|Valores|Descrição|
|-|-|-|
|**AccessToken**|Não configurado (padrão)|Modo de autenticação determinado por outras palavras-chave. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md). |
||Uma cadeia de caracteres de byte|O Azure AD Token de acesso extraídos de uma resposta de JSON do OAuth. A cadeia de caracteres de conexão não deve conter a ID de usuário, senha ou a palavra-chave de autenticação (requer o Driver ODBC versão 17 ou acima no Linux ou macOS). |
|**Autenticação**|Não configurado (padrão)|Modo de autenticação determinado por outras palavras-chave. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Autenticar diretamente a uma instância do SQL Server (que pode ser uma instância do Azure) usando um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando o **UID** e **PWD** palavras-chave. |
||`ActiveDirectoryPassword`|Autenticar com uma identidade do Active Directory do Azure usando um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando o **UID** e **PWD** palavras-chave. |
||`ActiveDirectoryMsi`|Autenticar usando uma identidade gerenciada atribuído pelo sistema ou uma identidade atribuída pelo usuário gerenciada (requer o Driver ODBC versão 17.3.1.1 ou superior). Para obter uma visão geral e tutoriais, consulte [What ' s identidades gerenciadas para recursos do Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).|

O **autenticação** palavra-chave afeta as configurações de segurança de conexão. Se ele for definido na cadeia de conexão e, em seguida, por padrão o **Encrypt** palavra-chave for definida como true, o que significa que o cliente solicita criptografia. Além disso, o certificado do servidor será validado, independentemente da configuração de criptografia, a menos que **TrustServerCertificate** é definido como true (**falso** por padrão). Esse recurso é diferenciado da antiga, menos o método de logon seguro, no qual o certificado do servidor é validado somente quando a criptografia é especificamente solicitada na cadeia de conexão.

Ao usar o Azure AD com os drivers PHP para SQL Server no Windows, você pode ser solicitado a instalar o [assistente Microsoft Online Services entrar](https://www.microsoft.com/download/details.aspx?id=41950) (não obrigatório para ODBC 17 +).

#### <a name="limitations"></a>Limitações

No Windows, o driver ODBC subjacente dá suporte a um valor mais para o **autenticação** palavra-chave **ActiveDirectoryIntegrated**, mas os drivers PHP não oferece suporte a esse valor em qualquer plataforma.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>Exemplo - conectar-se usando SqlPassword e ActiveDirectoryPassword

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>Exemplo - conectar-se usando o driver PDO_SQLSRV

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>Exemplo - conectar-se usando o Token de acesso do AD do Azure

### <a name="sqlsrv-driver"></a>Driver SQLSRV

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdosqlsrv-driver"></a>Driver PDO_SQLSRV

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>Exemplo - conectar-se usando identidades gerenciadas para recursos do Azure

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>Usando a identidade gerenciada atribuído pelo sistema com o driver SQLSRV

Ao conectar-se usando o atribuído pelo sistema de identidade gerenciada, não use as opções de UID ou PWD.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>Usando a identidade atribuída pelo usuário gerenciada com o driver PDO_SQLSRV

Uma identidade atribuída pelo usuário gerenciada é criada como um recurso autônomo do Azure. O Azure cria uma identidade no locatário do AD do Azure que é confiável para a assinatura em uso. Depois que a identidade é criada, a identidade pode ser atribuída a uma ou mais instâncias de serviço do Azure. Copie o `Object ID` dessa identidade e set-como o usuário o nome na cadeia de conexão. 

Portanto, quando se conectar usando o usuário atribuído identidade gerenciada, forneça a ID de objeto como o nome de usuário mas omitir a senha.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>Consulte Também
[Usando o Azure Active Directory com o Driver ODBC](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)

[O que é gerenciadas identidades para recursos do Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
