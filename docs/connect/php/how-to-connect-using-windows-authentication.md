---
title: 'Como: conectar-se usando a autenticação do Windows | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a1e43874edbdf5cc3ece40a141f3b32b7fe121e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-connect-using-windows-authentication"></a>Como se conectar usando a Autenticação do Windows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Por padrão, os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] usam a Autenticação do Windows para se conectar ao SQL Server. É importante observar que na maioria dos cenários, isso significa que o identidade de processo do servidor Web ou a identidade do thread (se o servidor Web estiver usando representação) é usada para se conectar ao servidor, não a identidade de um usuário final.  
  
Os seguintes pontos devem ser considerados ao usar a Autenticação do Windows para se conectar ao SQL Server:  
  
-   As credenciais usadas na execução do processo (ou thread) do servidor Web devem estar mapeadas a um logon válido do SQL Server para que a conexão seja estabelecida.  
  
-   Se o SQL Server e o servidor Web estiverem em computadores diferentes, o SQL Server deve ser configurado para permitir conexões remotas.  
  
> [!NOTE]  
> Atributos de conexão como *Database* e *ConnectionPooling* podem ser definidas ao estabelecer uma conexão. Para obter uma lista completa dos atributos de conexão com suporte, consulte [Connection Options](../../connect/php/connection-options.md).  
  
A Autenticação do Windows deve ser usada para se conectar ao SQL Server sempre que possível, pelos seguintes motivos:  
  
-   Nenhuma credencial é passada pela rede durante a Autenticação; nomes de usuário e senhas não são incorporadas na cadeia de conexão de banco de dados. Isso significa que usuários mal-intencionados ou invasores não podem obter as credenciais monitorando a rede ou exibindo cadeias de conexão nos arquivos de configuração.  
  
-   Os usuários estão sujeitos ao gerenciamento de contas centralizado e políticas de segurança, como períodos de validade da senha, comprimento mínimo da senha e bloqueio de conta após várias solicitações de logon inválidas, são impostas.  
  
Se a Autenticação do Windows não é uma opção prática, consulte [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa o driver SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]com Autenticação do Windows para se conectar a uma instância local do SQL Server. Depois que a conexão tiver sido estabelecida, o servidor será consultado para o logon do usuário que está acessando o banco de dados.  
  
O exemplo supõe que SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída é gravada no navegador quando o exemplo é executado do navegador.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa o driver PDO_SQLSRV para executar a mesma tarefa do exemplo anterior.  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Como se conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Programação de guia para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)

[Como: criar um logon do SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)

[Como: criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md)

[Gerenciando usuários, funções e logons](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Separação do esquema de usuário](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Conceder permissões de objeto (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
