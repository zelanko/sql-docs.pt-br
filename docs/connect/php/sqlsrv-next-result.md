---
title: sqlsrv_next_result | Microsoft Docs
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
apiname: sqlsrv_next_result
apitype: NA
helpviewer_keywords:
- multiple result sets
- sqlsrv_next_result
- stored procedure support
- API Reference, sqlsrv_next_result
ms.assetid: 41270d16-0003-417c-b837-ea51439654cd
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb34a1e134bf13f797157fbe49d1cb210fb4f036
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlsrvnextresult"></a>sqlsrv_next_result
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ativa o próximo resultado (conjunto de resultados, contagem de linhas ou parâmetro de saída) da instrução especificada.  
  
> [!NOTE]  
> O primeiro (ou único) resultado retornado por uma consulta em lotes ou procedimento armazenado está ativo sem uma chamada para **sqlsrv_next_result**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_next_result( resource $stmt )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: a instrução executada na qual o próximo resultado fica ativo.  
  
## <a name="return-value"></a>Valor de retorno  
Se o próximo resultado tiver sido ativado com êxito, o valor booliano **true** será retornado. Se ocorrer um erro na ativação do próximo resultado, **false** será retornado. Se não houver mais resultados disponíveis, **null** será retornado.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir cria e executa um procedimento armazenado que insere uma análise do produto na tabela *Production.ProductReview* e depois seleciona todas as análises do produto especificado. Após a execução do procedimento armazenado, o primeiro resultado (o número de linhas afetadas pela consulta INSERT no procedimento armazenado) é consumido sem chamar **sqlsrv_next_result**. O próximo resultado (as linhas retornadas pela consulta SELECT no procedimento armazenado) é disponibilizado chamando **sqlsrv_next_result** e consumido usando [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
> [!NOTE]  
> Chamar os procedimentos armazenados usando a sintaxe canônica é a prática recomendada. Para obter mais informações sobre a sintaxe canônica, consulte [Chamando um procedimento armazenado](http://go.microsoft.com/fwlink/?linkid=119517).  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado a partir da linha de comando.  
  
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
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('InsertProductReview', 'P') IS NOT NULL  
                DROP PROCEDURE InsertProductReview";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = " CREATE PROCEDURE InsertProductReview  
                                    @ProductID int,  
                                    @ReviewerName nvarchar(50),  
                                    @ReviewDate datetime,  
                                    @EmailAddress nvarchar(50),  
                                    @Rating int,  
                                    @Comments nvarchar(3850)  
                   AS  
                       BEGIN  
                             INSERT INTO Production.ProductReview   
                                         (ProductID,  
                                          ReviewerName,  
                                          ReviewDate,  
                                          EmailAddress,  
                                          Rating,  
                                          Comments)  
                                    VALUES  
                                         (@ProductID,  
                                          @ReviewerName,  
                                          @ReviewDate,  
                                          @EmailAddress,  
                                          @Rating,  
                                          @Comments);  
                             SELECT * FROM Production.ProductReview  
                                WHERE ProductID = @ProductID;  
                       END";  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
  
if( $stmt2 === false)  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
/*-------- The next few steps call the stored procedure. --------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of the  
parameters to be passed to the stored procedure */  
$tsql_callSP = "{call InsertProductReview(?, ?, ?, ?, ?, ?)}";  
  
/* Define the parameter array. */  
$productID = 709;  
$reviewerName = "Customer Name";  
$reviewDate = "2008-02-12";  
$emailAddress = "customer@email.com";  
$rating = 3;  
$comments = "[Insert comments here.]";  
$params = array(   
                 $productID,  
                 $reviewerName,  
                 $reviewDate,  
                 $emailAddress,  
                 $rating,  
                 $comments  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false)  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Consume the first result (rows affected by INSERT query in the  
stored procedure) without calling sqlsrv_next_result. */  
echo "Rows affectd: ".sqlsrv_rows_affected($stmt3)."-----\n";  
  
/* Move to the next result and display results. */  
$next_result = sqlsrv_next_result($stmt3);  
if( $next_result )  
{  
     echo "\nReview information for product ID ".$productID.".---\n";  
     while( $row = sqlsrv_fetch_array( $stmt3, SQLSRV_FETCH_ASSOC))  
     {  
          echo "ReviewerName: ".$row['ReviewerName']."\n";  
          echo "ReviewDate: ".date_format($row['ReviewDate'],  
                                             "M j, Y")."\n";  
          echo "EmailAddress: ".$row['EmailAddress']."\n";  
          echo "Rating: ".$row['Rating']."\n\n";  
     }  
}  
elseif( is_null($next_result))  
{  
     echo "No more results.\n";  
}  
else  
{  
     echo "Error in moving to next result.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
?>  
```  
  
Ao executar um procedimento armazenado que tenha parâmetros de saída, é recomendável que todos os outros resultados sejam consumidos antes de acessar os valores dos parâmetros de saída. Para obter mais informações, consulte [Como especificar a direção do parâmetro com o driver SQLSRV](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir executa uma consulta em lotes que recupera informações de análise de produto de uma ID de produto especificada, insere uma análise e depois, novamente, recupera as informações de análise da ID de produto especificada. A análise do produto recém-inserida será incluída no conjunto de resultados final da consulta em lotes. O exemplo usa [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md) para ir de um resultado da consulta em lotes para o seguinte.  
  
> [!NOTE]  
> O primeiro (ou único) resultado retornado por uma consulta em lotes ou procedimento armazenado está ativo sem uma chamada para **sqlsrv_next_result**.  
  
O exemplo usa a tabela *Purchasing.ProductReview* do banco de dados [AdventureWorks](http://go.microsoft.com/fwlink/?linkid=67739) e supõe que esse banco de dados esteja instalado no servidor. Toda a saída será gravada no console quando o exemplo for executado a partir da linha de comando.  
  
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
  
/* Define the batch query. */  
$tsql = "--Query 1  
         SELECT ProductID, ReviewerName, Rating   
         FROM Production.ProductReview   
         WHERE ProductID=?;  
  
         --Query 2  
         INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,   
                                               ReviewDate,   
                                               EmailAddress,   
                                               Rating)  
         VALUES (?, ?, ?, ?, ?);  
  
         --Query 3  
         SELECT ProductID, ReviewerName, Rating   
         FROM Production.ProductReview   
         WHERE ProductID=?;";  
  
/* Assign parameter values and execute the query. */  
$params = array(798,   
                798,   
                'CustomerName',   
                '2008-4-15',   
                'test@customer.com',   
                3,   
                798 );  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the first result. */  
echo "Query 1 result:\n";  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC ))  
{  
     print_r($row);  
}  
  
/* Move to the next result of the batch query. */  
sqlsrv_next_result($stmt);  
  
/* Display the result of the second query. */  
echo "Query 2 result:\n";  
echo "Rows Affected: ".sqlsrv_rows_affected($stmt)."\n";  
  
/* Move to the next result of the batch query. */  
sqlsrv_next_result($stmt);  
  
/* Retrieve and display the third result. */  
echo "Query 3 result:\n";  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC ))  
{  
     print_r($row);  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)  
[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
[Recuperando dados](../../connect/php/retrieving-data.md)  
[Atualizando dados &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Aplicativo de exemplo &#40;driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
