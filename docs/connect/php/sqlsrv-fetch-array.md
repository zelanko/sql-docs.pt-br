---
title: sqlsrv_fetch_array | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_fetch_array
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_array
- retrieving data, as an array
- API Reference, sqlsrv_fetch_array
ms.assetid: 69270b9e-0791-42f4-856d-412da39dea63
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aab41821d2f4eb1eb3f92ce998fe440593567d0a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979709"
---
# <a name="sqlsrvfetcharray"></a>sqlsrv_fetch_array
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera a próxima linha de dados como uma matriz indexada numericamente, matriz associativa ou ambas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_fetch_array( resource $stmt[, int $fetchType [, row[, ]offset]])  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: um recurso de instrução correspondente a uma instrução executada.  
  
*$fetchType* [OPCIONAL]: uma constante predefinida. Esse parâmetro pode assumir um dos valores listados na tabela a seguir:  
  
|Valor|Descrição|  
|---------|---------------|  
|SQLSRV_FETCH_NUMERIC|A próxima linha de dados é retornada como uma matriz numérica.|  
|SQLSRV_FETCH_ASSOC|A próxima linha de dados é retornada como uma matriz associativa. As chaves da matriz são os nomes das colunas no conjunto de resultados.|  
|SQLSRV_FETCH_BOTH|A próxima linha de dados é retornada tanto como uma matriz numérica quanto como uma matriz associativa. Este é o valor padrão.|  
  
*row* [OPCIONAL]: adicionado na versão 1.1. Um dos valores a seguir, especificando a linha a ser acessada em um conjunto de resultados que usa um cursor rolável. (Quando *row* for especificado, *fetchtype* deverá ser especificado explicitamente, mesmo se você especificar o valor padrão.)  
  
-   SQLSRV_SCROLL_NEXT  
-   SQLSRV_SCROLL_PRIOR  
-   SQLSRV_SCROLL_FIRST  
-   SQLSRV_SCROLL_LAST  
-   SQLSRV_SCROLL_ABSOLUTE  
-   SQLSRV_SCROLL_RELATIVE  
  
Para obter mais informações sobre esses valores, consulte [Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md). O suporte para cursor rolável foi adicionado na versão 1.1 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
*offset* [OPCIONAL]: usado com SQLSRV_SCROLL_ABSOLUTE e SQLSRV_SCROLL_RELATIVE para especificar a linha a ser recuperada. O primeiro registro no conjunto de resultados é 0.  
  
## <a name="return-value"></a>Valor retornado  
Se uma linha de dados for recuperada, uma **matriz** será retornada. Se não houver mais linhas para recuperar, **null** será retornado. Se ocorrer um erro, **false** será retornado.  
  
Com base no valor do parâmetro *$fetchType* retornado, a **matriz** retornada poderá ser uma **matriz**indexada numericamente, uma **matriz**associativa ou ambas. Por padrão, uma **matriz** com chaves numéricas e associativas é retornada. O tipo de dados de um valor na matriz retornada será o tipo de dados do PHP padrão. Para obter informações sobre os tipos de dados padrão do PHP, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="remarks"></a>Remarks  
Se uma coluna sem nome for retornada, a chave associativa do elemento da matriz será uma cadeia de caracteres vazia (""). Por exemplo, considere esta instrução Transact-SQL que insere um valor em uma tabela de banco de dados e recupera a chave primária gerada pelo servidor:  
  
```
INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()
```
  
Se o conjunto de resultados retornado pela parte `SELECT SCOPE_IDENTITY()` dessa instrução for recuperado como uma matriz associativa, a chave do valor retornado será uma cadeia de caracteres vazia ("") porque a coluna retornada não tem nome. Para evitar isso, você pode recuperar o resultado como uma matriz numérica ou pode especificar um nome para a coluna retornada na instrução Transact-SQL. Veja a seguir uma maneira de especificar um nome de coluna no Transact-SQL:  
  
```
SELECT SCOPE_IDENTITY() AS PictureID
```
  
Se um conjunto de resultados contiver várias colunas sem nome, o valor da última coluna sem nome será atribuído à chave da cadeia de caracteres vazia ("").  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir recupera cada linha de um conjunto de resultados como uma **matriz**associativa. O exemplo supõe que o SQL Server e o banco de dados do [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as an associative array and display the results.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_ASSOC))  
{  
      echo $row['LastName'].", ".$row['FirstName']."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir recupera cada linha de um conjunto de resultados como uma matriz indexada numericamente.  
  
O exemplo recupera informações de produtos da tabela *Purchasing.PurchaseOrderDetail* do banco de dados AdventureWorks para produtos que tenham uma data especificada e uma quantidade em estoque (*StockQty*) menor que um valor especificado.  
  
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
  
/* Define the query. */  
$tsql = "SELECT ProductID,  
                UnitPrice,  
                StockedQty   
         FROM Purchasing.PurchaseOrderDetail  
         WHERE StockedQty < 3   
         AND DueDate='2002-01-29'";  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set printing a row of data upon each  
iteration.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC))  
{  
     echo "ProdID: ".$row[0]."\n";  
     echo "UnitPrice: ".$row[1]."\n";  
     echo "StockedQty: ".$row[2]."\n";  
     echo "-----------------\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
A função **sqlsrv_fetch_array** sempre retorna dados de acordo com os [Default PHP Data Types](../../connect/php/default-php-data-types.md). Para obter informações sobre como especificar o tipo de dados do PHP, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Se um campo sem nome for recuperado, a chave associativa do elemento da matriz será uma cadeia de caracteres vazia (""). Para obter mais informações, consulte [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Recuperando dados](../../connect/php/retrieving-data.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)

[Guia de programação para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
