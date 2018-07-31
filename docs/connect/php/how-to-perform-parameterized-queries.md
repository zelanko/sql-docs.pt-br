---
title: 'Como: executar consultas parametrizadas | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6095a83f4bb9982a929e0bb41e7269bc6e41935
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38032985"
---
# <a name="how-to-perform-parameterized-queries"></a>Como executar consultas parametrizadas
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico resume e demonstra como usar os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para executar uma consulta parametrizada.  
  
As etapas para executar uma consulta parametrizada podem ser resumidas em quatro etapas:  
  
1.  Coloque pontos de interrogação (?) como espaços reservados de parâmetros na cadeia de caracteres Transact-SQL que é a consulta a ser executada.  
  
2.  Inicialize ou atualize as variáveis do PHP correspondentes aos espaços reservados na consulta Transact-SQL.  
  
3.  Use as variáveis do PHP da etapa 2 para criar ou atualizar uma matriz de valores de parâmetros que correspondem aos espaços reservados do parâmetro na cadeia de caracteres Transact-SQL. Os valores de parâmetro na matriz devem ser na mesma ordem que os espaços reservados significava para representá-los.
  
4.  Execute a consulta:  
  
    -   Se você estiver usando o driver SQLSRV, use [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
    -   Se você estiver usando o driver PDO_SQLSRV, execute a consulta com [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md). Os tópicos para [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md) têm exemplos de código.  
  
O restante deste tópico discute consultas parametrizadas usando o driver SQLSRV.  
  
> [!NOTE]  
> Os parâmetros são associados implicitamente usando **sqlsrv_prepare**. Isso significa que, se uma consulta parametrizada for preparada usando **sqlsrv_prepare** e os valores na matriz de parâmetros forem atualizados, esses valores atualizados serão usados na próxima execução da consulta. Consulte o segundo exemplo neste tópico para obter mais detalhes.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir atualiza a quantidade de uma identificação de produto especificada na tabela *Production.ProductInventory* do banco de dados AdventureWorks. A quantidade e a identificação do produto são parâmetros na consulta UPDATE.  
  
O exemplo, então, consulta o banco de dados para verificar se a quantidade foi atualizada corretamente. A identificação do produto é um parâmetro na consulta SELECT.  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
O exemplo anterior usa a função **sqlsrv_query** para executar consultas. Essa função é útil para executar consultas únicas, pois efetua a preparação e a execução da instrução. A combinação de **sqlsrv_prepare**/**sqlsrv_execute** é recomendada para executar novamente uma consulta com valores de parâmetros diferentes. Para ver um exemplo de nova execução de uma consulta com valores de parâmetros diferentes, consulte o exemplo a seguir.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir demonstra a associação implícita de variáveis ao usar a função **sqlsrv_prepare** . O exemplo insere várias ordens de venda na tabela *Sales.SalesOrderDetail* . A matriz *$params* é associada à instrução *$stmt* quando **sqlsrv_prepare** é chamado. Antes de cada execução de uma consulta que insere uma nova ordem de venda na tabela, a matriz *$params* é atualizada com novos valores correspondentes aos detalhes da ordem de venda. A próxima execução da consulta usa os novos valores de parâmetro.  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Convertendo tipos de dados](../../connect/php/converting-data-types.md)

[Considerações de segurança para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/security-considerations-for-php-sql-driver.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  
