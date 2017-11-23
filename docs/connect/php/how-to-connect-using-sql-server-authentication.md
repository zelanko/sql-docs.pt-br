---
title: "Como: conectar-se usando a autenticação do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
caps.latest.revision: "34"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5802ddf79f53fda9e03c842ce21def20cb99f6e3
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-connect-using-sql-server-authentication"></a>Como se conectar usando a Autenticação do SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] oferece suporte à Autenticação do SQL Server quando você se conecta ao SQL Server.  
  
A Autenticação do SQL Server deve ser usada somente quando a Autenticação do Windows não for possível. Para obter informações sobre a conexão com a Autenticação do Windows, consulte [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Os seguintes pontos devem ser considerados ao usar a Autenticação do SQL Server para se conectar ao SQL Server:  
  
-   A Autenticação de modo misto do SQL Server deve estar habilitada no servidor.  
  
-   A ID de usuário e senha (*UID* e *PWD* atributos de conexão no driver SQLSRV) devem ser definidas quando você tentar estabelecer uma conexão. A ID de usuário e a senha devem mapear para um usuário e uma senha válidos do SQL Server.  
  
> [!NOTE]  
> Em senhas contendo uma chave de fechamento (}), uma segunda chave de fechamento deverá ser incluída. Por exemplo, se a senha do SQL Server for "pass} word", o valor do atributo de conexão *PWD* deve ser definido como "pass}} word".  
  
As seguintes precauções devem ser tomadas ao usar a Autenticação do SQL Server para se conectar ao SQL Server:  
  
-   Proteger (criptografar) as credenciais passadas pela rede do servidor Web para o banco de dados. As credenciais são criptografadas por padrão desde o SQL Server 2005. Para maior segurança, defina o atributo de conexão Encrypt como "on" para criptografar todos os dados enviados ao servidor.  
  
> [!NOTE]  
> Quando você define o atributo de conexão Encrypt como "on", pode haver diminuição do desempenho, pois a criptografia de dados pode demandar um uso intensivo dos recursos computacionais.  
  
-   Não inclua valores para os atributos de conexão *UID* e *PWD* em texto sem formatação em scripts do PHP. Esses valores devem ser armazenados em um diretório específico do aplicativo com as permissões restritas apropriadas.  
  
-   Evite usar a conta *sa* . Mapeie o aplicativo para um usuário de banco de dados com os privilégios desejados e use uma senha forte.  
  
> [!NOTE]  
> Os atributos de conexão, a ID de usuário e a senha podem ser definidos ao estabelecer uma conexão. Para obter uma lista completa dos atributos de conexão com suporte, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa o driver SQLSRV com Autenticação do SQL Server para se conectar a uma instância local do SQL Server. Os valores para o *UID* e *PWD* atributos de conexão são obtidos de arquivos de texto específicos do aplicativo, *uid.txt* e *pwd.txt*, além de *C:\AppData* directory. Depois que a conexão é estabelecida, o servidor é consultado para verificar o logon do usuário.  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) estejam instalados no computador local. Toda a saída é gravada no navegador quando o exemplo é executado do navegador.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
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
Este exemplo usa o driver PDO_SQLSRV para demonstrar como se conectar com a Autenticação do SQL Server.  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
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
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
[Suser_sname (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=106382)  
[Como criar um logon do SQL Server](http://go.microsoft.com/fwlink/?LinkId=106325)  
[Como criar um usuário de banco de dados](http://go.microsoft.com/fwlink/?LinkId=106327)  
[Gerenciando usuários, funções e logons](http://go.microsoft.com/fwlink/?LinkId=106329)  
[Separação do esquema de usuário](http://go.microsoft.com/fwlink/?LinkId=106330)  
[Conceder permissões de objeto (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=106332)  
  
