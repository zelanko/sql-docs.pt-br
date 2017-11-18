---
title: sqlsrv_execute | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_execute
apitype: NA
helpviewer_keywords:
- sqlsrv_exclude
- executing queries
- API Reference, sqlsrv_execute
ms.assetid: 38331bc2-4391-4f9f-aa83-9873dad605a0
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d9326e49d0fd22440fe8d974d7d0b66800e04cdc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvexecute"></a>sqlsrv_execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Executa uma instrução preparada anteriormente. Consulte [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) para obter informações sobre como preparar uma instrução para execução.  
  
> [!NOTE]  
> Essa função é ideal para executar uma instrução preparada várias vezes com valores de parâmetros diferentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_execute( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: um recurso que especifica a instrução a ser executada. Para obter mais informações sobre como criar um recurso de instrução, consulte [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
## <a name="return-value"></a>Valor de retorno  
Um valor booliano: **true** se a instrução foi executada com êxito. Caso contrário, **false**.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir executa uma instrução que atualiza um campo na tabela *Sales.SalesOrderDetail* do banco de dados [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) . O exemplo supõe que o SQL Server e o banco de dados AdventureWorks estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ( ?)   
         WHERE SalesOrderDetailID = ( ?)";  
  
/* Set up the parameters array. Parameters correspond, in order, to  
question marks in $tsql. */  
$params = array( 5, 10);  
  
/* Create the statement. */  
$stmt = sqlsrv_prepare( $conn, $tsql, $params);  
if( $stmt )  
{  
     echo "Statement prepared.\n";  
}  
else  
{  
     echo "Error in preparing statement.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute the statement. Display any errors that occur. */  
if( sqlsrv_execute( $stmt))  
{  
      echo "Statement executed.\n";  
}  
else  
{  
     echo "Error in executing statement.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)  
[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
[sqlsrv_query](../../connect/php/sqlsrv-query.md)  
  

