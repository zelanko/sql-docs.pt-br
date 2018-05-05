---
title: 'Como: especificar tipos de dados do PHP | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fdd7d2eee34303c466da0445233109b707c6645
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-specify-php-data-types"></a>Como especificar tipos de dados do PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ao usar o driver PDO_SQLSRV, você pode especificar o tipo de dados do PHP ao recuperar dados do servidor com PDOStatement::bindColumn e PDOStatement::bindParam. Consulte [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) e [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) para obter mais informações.  
  
As etapas a seguir resumem como especificar tipos de dados do PHP ao recuperar dados do servidor usando o driver SQLSRV:  
  
1.  Configurar e executar uma consulta Transact-SQL com [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou uma combinação de [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
2.  Disponibilize a próxima linha de dados para leitura com [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md).  
  
3.  Recupere os dados de um campo de uma linha retornada usando [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) com o tipo de dados do PHP desejado especificado como o terceiro parâmetro opcional. Se o terceiro parâmetro opcional não for especificado, dados são retornados de acordo com os tipos do PHP padrão. Para obter informações sobre tipos do PHP retornados padrão, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
    Para obter informações sobre as constantes usadas para especificar o tipo de dados do PHP, consulte a seção PHPTYPEs de [constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir recupera linhas da tabela *Production.ProductReview* do banco de dados AdventureWorks. Em cada linha retornada, o *ReviewDate* campo é recuperado como uma cadeia de caracteres e o *comentários* campo é recuperado como um fluxo. Os dados de fluxo são exibidos com o uso da função [fpassthru](http://php.net/manual/en/function.fpassthru.php) do PHP.  
  
O exemplo supõe que SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT ReviewerName,   
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
No exemplo, a recuperação do segundo campo (*ReviewDate*) como uma cadeia de caracteres preserva a precisão de milissegundos do tipo de dados DATETIME do SQL Server. Por padrão, o tipo de dados DATETIME do SQL Server é recuperado como um objeto DateTime do PHP, no qual a precisão de milissegundos é perdida.  
  
Recuperação do quarto campo (*comentários*) como um fluxo para fins de demonstração. Por padrão, o tipo de dados nvarchar (3850) do SQL Server é recuperado como uma cadeia de caracteres, que é aceitável para a maioria das situações.  
  
> [!NOTE]  
> A função [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) fornece uma maneira de obter informações de campo, incluindo informações de tipo, antes de executar uma consulta.  
  
## <a name="see-also"></a>Consulte também  
[Recuperando dados](../../connect/php/retrieving-data.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)

[Como recuperar parâmetros de saída usando o driver SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
