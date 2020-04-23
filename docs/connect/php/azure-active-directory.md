---
title: Azure Active Directory
description: Saiba como usar a autenticação do Azure Active Directory com os Microsoft Drivers for PHP for SQL Server.
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac1e598b5599caa9020ed795d1bffd185887ad76
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81625456"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Conectar usando a Autenticação do Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[O Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure Active Directory) é uma tecnologia de gerenciamento de ID de usuário central que funciona como uma alternativa para a [autenticação do SQL Server](how-to-connect-using-sql-server-authentication.md). O Azure AD permite conexões com Banco de Dados SQL do Microsoft Azure e SQL Data Warehouse com identidades federadas no Azure AD usando um nome de usuário e senha, autenticação integrada do Windows ou um token de acesso do Azure AD. Os drivers do PHP para SQL Server oferecem suporte parcial para esses recursos.

Para usar o Azure AD, use as palavras-chave **Authentication** ou **AccessToken** (elas são mutuamente exclusivas), conforme mostrado na tabela a seguir. Para obter mais detalhes técnicos, confira [Usar o Azure Active Directory com o Driver ODBC](../odbc/using-azure-active-directory.md).

|Palavra-chave|Valores|Descrição|
|-|-|-|
|**AccessToken**|Não definido (padrão)|Modo de autenticação determinado por outras palavras-chave. Para obter mais informações, consulte [Connection Options](connection-options.md). |
||Uma cadeia de caracteres de byte|O token de acesso do Azure AD extraído de uma resposta JSON do OAuth. A cadeia de conexão não deve conter a ID de usuário, a senha ou a palavra-chave de autenticação (requer o Driver ODBC versão 17 ou superior no Linux ou no macOS). |
|**Autenticação**|Não definido (padrão)|Modo de autenticação determinado por outras palavras-chave. Para obter mais informações, consulte [Connection Options](connection-options.md). |
||`SqlPassword`|Autentique diretamente em uma instância do SQL Server (que pode ser uma instância do Azure) usando um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando as palavras-chave **UID** e **PWD**. |
||`ActiveDirectoryPassword`|Autentique com a identidade do Azure Active Directory por meio de um nome de usuário e senha. O nome de usuário e a senha devem ser passados para a cadeia de conexão usando as palavras-chave **UID** e **PWD**. |
||`ActiveDirectoryMsi`|Autentique usando uma identidade gerenciada atribuída pelo sistema ou uma identidade gerenciada atribuída pelo usuário (requer o Driver ODBC versão 17.3.1.1 ou superior). Para obter uma visão geral e tutoriais, confira [O que são identidades gerenciadas para recursos do Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).|

A palavra-chave **Autenticação** afeta as configurações de segurança da conexão. Se ela for definida na cadeia de conexão, então, por padrão, a palavra-chave **Criptografar** será definida como true, o que significa que o cliente solicitará criptografia. Além disso, o certificado do servidor será validado independentemente da configuração de criptografia, a menos que **TrustServerCertificate** seja definido como true (ele é **false** por padrão). Esse recurso é diferenciado do método de logon antigo e menos seguro, no qual o certificado do servidor é validado somente quando a criptografia é expressamente solicitada na cadeia de conexão.

#### <a name="limitations"></a>Limitações

No Windows, o driver ODBC subjacente é compatível com mais um valor para a palavra-chave **Autenticação**, **ActiveDirectoryIntegrated**, mas os drivers PHP não são compatíveis com esse valor em nenhuma plataforma.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>Exemplo – conectar usando SqlPassword e ActiveDirectoryPassword

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

## <a name="example---connect-using-the-pdo_sqlsrv-driver"></a>Exemplo – conectar usando o driver PDO_SQLSRV

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

## <a name="example---connect-using-azure-ad-access-token"></a>Exemplo – conectar usando o token de acesso do Azure AD

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

### <a name="pdo_sqlsrv-driver"></a>Driver PDO_SQLSRV

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>Exemplo – conectar usando identidades gerenciadas para recursos do Azure

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>Usar a identidade gerenciada atribuída pelo sistema com o driver SQLSRV

Ao se conectar usando a identidade gerenciada atribuída pelo sistema, não use as opções UID ou PWD.

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

### <a name="using-the-user-assigned-managed-identity-with-pdo_sqlsrv-driver"></a>Usar a identidade gerenciada atribuída pelo sistema com o driver PDO_SQLSRV

Uma identidade gerenciada atribuída pelo usuário é criada como um recurso autônomo do Azure. O Azure cria uma identidade no locatário do Azure AD que inspira confiança na assinatura em uso. Depois que a identidade é criada, ela pode ser atribuída a uma ou mais instâncias de serviço do Azure. Copie o `Object ID` dessa identidade e defina-o como o nome de usuário na cadeia de conexão. 

Portanto, ao se conectar usando a identidade gerenciada atribuída pelo usuário, forneça a ID de Objeto como o nome de usuário, mas omita a senha.

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
[Usando o Azure Active Directory com o Driver ODBC](../odbc/using-azure-active-directory.md)

[O que são identidades gerenciadas para recursos do Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
