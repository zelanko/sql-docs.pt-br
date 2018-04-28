---
title: sqlsrv_num_fields | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- sqlsrv_num_fields
apitype: NA
helpviewer_keywords:
- sqlsrv_num_fields
- API Reference, sqlsrv_num_fields
ms.assetid: 03ca1860-01ed-408c-862a-57a7355de4bf
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c14e51cba2ee57a32c18a8d87593b311fffc832
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsrvnumfields"></a>sqlsrv_num_fields
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera o número de campos em um conjunto de resultados ativo. Essa função pode ser chamada em qualquer instrução preparada, antes ou após a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_num_fields( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: a instrução na qual o conjunto de resultados de destino está ativo.  
  
## <a name="return-value"></a>Valor de retorno  
Um valor inteiro que representa o número de campos no conjunto de resultados ativo. Se ocorrer um erro, será retornado o valor booliano **false** .  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir executa uma consulta para recuperar todos os campos para as três primeiras linhas no *HumanResources. Department* tabela do banco de dados AdventureWorks. A função **sqlsrv_num_fields** determina o número de campos no conjunto de resultados. Isso permite que os dados sejam exibidos pela iteração dos campos em cada linha retornada.  
  
O exemplo supõe que SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
/* Define and execute the query. */  
$tsql = "SELECT TOP (3) * FROM HumanResources.Department";  
$stmt = sqlsrv_query($conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in executing query.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the number of fields. */  
$numFields = sqlsrv_num_fields( $stmt );  
  
/* Iterate through each row of the result set. */  
while( sqlsrv_fetch( $stmt ))  
{  
     /* Iterate through the fields of each row. */  
     for($i = 0; $i < $numFields; $i++)  
     {  
          echo sqlsrv_get_field($stmt, $i,   
                   SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))." ";  
     }  
     echo "\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
