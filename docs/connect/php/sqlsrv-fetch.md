---
description: sqlsrv_fetch
title: sqlsrv_fetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_fetch
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch
- API Reference, sqlsrv_fetch
- retrieving data, as a single field
ms.assetid: a5a640a1-6e7d-452e-8b66-850a4dc2ce89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eeff60b0e5d685021300a2b2272ece8aa8264dd7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487868"
---
# <a name="sqlsrv_fetch"></a>sqlsrv_fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Disponibiliza a próxima linha de um conjunto de resultados para leitura. Use [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) para ler os campos da linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_fetch( resource $stmt[, row[, ]offset])  
```  
  
#### <a name="parameters"></a>parâmetros  
*$stmt*: um recurso de instrução correspondente a uma instrução executada.  
  
> [!NOTE]  
> Uma instrução deve ser executada antes que os resultados possam ser recuperados. Para obter informações sobre como executar uma instrução, consulte [sqlsrv_query](../../connect/php/sqlsrv-query.md) e [sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
*row* [OPCIONAL]: um dos valores a seguir que especifica a linha a ser acessada em um conjunto de resultados que usa um cursor rolável:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Para obter mais informações sobre esses valores, consulte [Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
*offset* [OPCIONAL]: usado com SQLSRV_SCROLL_ABSOLUTE e SQLSRV_SCROLL_RELATIVE para especificar a linha a ser recuperada. O primeiro registro no conjunto de resultados é 0.  
  
## <a name="return-value"></a>Valor retornado  
Se a próxima linha do conjunto de resultados for recuperada com êxito, **true** será retornado. Se não houver mais nenhum resultado no conjunto de resultados, **null** será retornado. Se ocorrer um erro, **false** será retornado.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa **sqlsrv_fetch** para recuperar uma linha de dados que contém uma análise do produto e o nome do revisor. Para recuperar dados do conjunto de resultados, [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) é usado. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up and execute the query. Note that both ReviewerName and  
Comments are of SQL Server type nvarchar. */  
$tsql = "SELECT ReviewerName, Comments   
         FROM Production.ProductReview  
         WHERE ProductReviewID=1";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Make the first row of the result set available for reading. */  
if( sqlsrv_fetch( $stmt ) === false)  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Note: Fields must be accessed in order.  
Get the first field of the row. Note that no return type is  
specified. Data will be returned as a string, the default for  
a field of type nvarchar.*/  
$name = sqlsrv_get_field( $stmt, 0);  
echo "$name: ";  
  
/*Get the second field of the row as a stream.  
Because the default return type for a nvarchar field is a  
string, the return type must be specified as a stream. */  
$stream = sqlsrv_get_field( $stmt, 1,   
                            SQLSRV_PHPTYPE_STREAM( SQLSRV_ENC_CHAR));  
while( !feof( $stream ))  
{   
    $str = fread( $stream, 10000);  
    echo $str;  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Recuperando dados](../../connect/php/retrieving-data.md)  

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
