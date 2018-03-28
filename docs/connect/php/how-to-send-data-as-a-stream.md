---
title: 'Como: enviar dados como um fluxo | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- updating data
- streaming data
ms.assetid: ab6b95d6-b6e6-4bd7-a18c-50f2918f7532
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1821f922e9c45340365abf680f5f46a61d6eb1e
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-send-data-as-a-stream"></a>Como enviar dados como um fluxo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] aproveita os fluxos PHP para enviar objetos grandes para o servidor. Os exemplos neste tópico demonstram como enviar dados como fluxo. O primeiro exemplo usa o driver SQLSRV para demonstrar o comportamento padrão, que é enviar todos os dados do fluxo no momento da execução da consulta. O segundo exemplo usa o driver SQLSRV para demonstrar como enviar até oito quilobytes (8 kB) de fluxo de dados por vez para o servidor.  
  
O terceiro exemplo mostra como enviar dados de fluxo para o servidor usando o driver PDO_SQLSRV.  
  
## <a name="example-sending-stream-data-at-execution"></a>Exemplo: Enviar dados de fluxo em execução
O exemplo a seguir insere uma linha na tabela *Production.ProductReview* do banco de dados do AdventureWorks. Os comentários do cliente (*$comments*) são abertos como um fluxo com o PHP [fopen](http://php.net/manual/en/function.fopen.php) de função e, então, transmitidos para o servidor após a execução da consulta.  
  
O exemplo supõe que SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída é gravada no console.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Execute the query. All stream data is sent upon execution.*/  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
else  
{  
     echo "The query was successfully executed.";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example-sending-stream-data-using-sqlsrvsendstreamdata"></a>Exemplo: Enviar o fluxo de dados usando sqlsrv_send_stream_data
O exemplo a seguir é o mesmo que o exemplo anterior, mas o comportamento padrão de enviar todos os dados de fluxo em execução está desativado. O exemplo usa [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md) para enviar dados de fluxo para o servidor. Até oito quilobytes (8 kB) de dados é enviado com cada chamada para **sqlsrv_send_stream_data**. O script conta o número de chamadas feitas por **sqlsrv_send_stream_data** e exibe a contagem no console.  
  
O exemplo supõe que SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída é gravada no console.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Turn off the default behavior of sending all stream data at  
execution. */  
$options = array("SendStreamParamsAtExec" => 0);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params, $options);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Send up to 8K of parameter data to the server with each call to  
sqlsrv_send_stream_data. Count the calls. */  
$i = 1;  
while( sqlsrv_send_stream_data( $stmt))   
{  
     echo "$i call(s) made.\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Embora os exemplos neste tópico enviem dados de caractere para o servidor, é possível enviar dados em qualquer formato como fluxo. Por exemplo, você também pode usar as técnicas demonstradas neste tópico para enviar imagens em formato binário como fluxos.  
  
## <a name="example-sending-an-image-as-a-stream"></a>Exemplo: Envio de uma imagem como um fluxo 
  
```  
<?php  
   $server = "(local)";   
   $database = "Test";  
   $conn = new PDO( "sqlsrv:server=$server;Database = $database", "", "");  
  
   $binary_source = fopen( "data://text/plain,", "r");  
  
   $stmt = $conn->prepare("insert into binaries (imagedata) values (?)");  
   $stmt->bindParam(1, $binary_source, PDO::PARAM_LOB);   
  
   $conn->beginTransaction();  
   $stmt->execute();  
   $conn->commit();  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Atualizando dados &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Recuperando dados como um fluxo usando o driver SQLSRV](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
