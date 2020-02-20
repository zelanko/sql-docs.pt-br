---
title: 'Como fazer: Recuperar parâmetros de saída usando o driver SQLSRV | Microsoft Docs'
ms.custom: ''
ms.date: 04/11/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1157bab7-6ad1-4bdb-a81c-662eea3e7fcd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db1216f513f353a6c703805c7aabe7b8dd468115
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993403"
---
# <a name="how-to-retrieve-output-parameters-using-the-sqlsrv-driver"></a>Como fazer: Recuperar parâmetros de saída usando o driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico demonstra como chamar um procedimento armazenado no qual um parâmetro foi definido como parâmetro de saída. Ao recuperar um parâmetro de saída ou de entrada/saída, todos os resultados retornados pelo procedimento armazenado devem ser consumidos antes que o valor do parâmetro retornado esteja acessível.  
  
> [!NOTE]  
> Variáveis que são inicializadas ou atualizadas para **null**, **DateTime**ou tipos de fluxo não podem ser usadas como parâmetros de saída.  
  
Pode ocorrer truncamento de dados quando tipos de fluxo como SQLSRV_SQLTYPE_VARCHAR('max') são usados como parâmetros de saída. Não há suporte para tipos de fluxos como parâmetros de saída. Para tipos que não são de fluxo, poderá ocorrer truncamento de dados se o comprimento do parâmetro de saída não for especificado ou se o comprimento especificado não for grande o suficiente para o parâmetro de saída.  
  
## <a name="example-1"></a>Exemplo 1
O exemplo a seguir chama um procedimento armazenado que retorna as vendas acumuladas no ano por um funcionário especificado. A variável PHP *$lastName* é um parâmetro de entrada e *$salesYTD* é um parâmetro de saída.  
  
> [!NOTE]  
> Inicializar *$salesYTD* como 0.0 define o PHPTYPE retornado como **float**. Para garantir a integridade do tipo de dados, os parâmetros de saída devem ser inicializados antes de chamar o procedimento armazenado, ou o PHPTYPE desejado deve ser especificado. Para obter informações sobre como especificar o PHPTYPE, confira [Como especificar tipos de dados do PHP](../../connect/php/how-to-specify-php-data-types.md).  
  
Como apenas um resultado é retornado pelo procedimento armazenado, *$salesYTD* contém o valor retornado do parâmetro de saída imediatamente após o procedimento armazenado ser executado.  
  
> [!NOTE]  
> Chamar os procedimentos armazenados usando a sintaxe canônica é a prática recomendada. Para obter mais informações sobre a sintaxe canônica, veja [Como chamar um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
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
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('GetEmployeeSalesYTD', 'P') IS NOT NULL  
                DROP PROCEDURE GetEmployeeSalesYTD";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = " CREATE PROCEDURE GetEmployeeSalesYTD  
                   @SalesPerson nvarchar(50),  
                   @SalesYTD money OUTPUT  
                   AS  
                   SELECT @SalesYTD = SalesYTD  
                   FROM Sales.SalesPerson AS sp  
                   JOIN HumanResources.vEmployee AS e   
                   ON e.EmployeeID = sp.SalesPersonID  
                   WHERE LastName = @SalesPerson";  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
 the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call GetEmployeeSalesYTD( ?, ? )}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an OUTPUT  
parameter. Initializing $salesYTD to 0.0 sets the returned PHPTYPE to  
float. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
$lastName = "Blythe";  
$salesYTD = 0.0;  
$params = array(   
                 array($lastName, SQLSRV_PARAM_IN),  
                 array(&$salesYTD, SQLSRV_PARAM_OUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $salesYTD. */  
echo "YTD sales for ".$lastName." are ". $salesYTD. ".";  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  

> [!NOTE]
> Ao associar um parâmetro de saída a um tipo bigint, se o valor puder terminar fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), será necessário especificar seu tipo de campo SQL como SQLSRV_SQLTYPE_BIGINT. Caso contrário, isso poderá resultar em uma exceção de "valor fora do intervalo".

## <a name="example-2"></a>Exemplo 2
Este exemplo de código mostra como associar um valor bigint grande como um parâmetro de saída.  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"testDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume the stored procedure spTestProcedure exists, which retrieves a bigint value of some large number
// e.g. 9223372036854
$bigintOut = 0;
$outSql = "{CALL spTestProcedure (?)}";
$stmt = sqlsrv_prepare($conn, $outSql, array(array(&$bigintOut, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_BIGINT)));
sqlsrv_execute($stmt);
echo "$bigintOut\n";   // Expect 9223372036854

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>Consulte Também  
[Como: Especificar a direção do parâmetro usando o driver SQLSRV](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[Como: Recuperar parâmetros de entrada e de saída usando o driver SQLSRV](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)

[Recuperando dados](../../connect/php/retrieving-data.md)  
  
