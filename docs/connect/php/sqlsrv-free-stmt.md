---
title: sqlsrv_free_stmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_free_stmt
apitype: NA
helpviewer_keywords:
- sqlsrv_free_stmt
- API Reference, sqlsrv_free_stmt
ms.assetid: 3c71f432-36ad-41e1-8ac7-587c82539448
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fe1471d41bf7b510c52f584b538fde03d6c0c084
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802805"
---
# <a name="sqlsrvfreestmt"></a>sqlsrv_free_stmt
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Libera todos os recursos associados à instrução especificada. A instrução não pode ser usada novamente depois que essa função foi chamada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_free_stmt( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: a instrução a ser fechada.  
  
## <a name="return-value"></a>Valor retornado  
O valor booliano **true** , a menos que a função seja chamada com um parâmetro inválido. Se a função for chamada com um parâmetro inválido, **false** será retornado.  
  
> [!NOTE]  
> **Null** é um parâmetro válido para esta função. Isso permite que a função seja chamada várias vezes em um script. Por exemplo, se você liberar uma instrução em uma condição de erro e liberá-la novamente no final do script, a segunda chamada para **sqlsrv_free_stmt** retornará **true** porque a primeira chamada para **sqlsrv_free_stmt** (na condição de erro) define o recurso de conexão como **null**.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir cria um recurso de instrução, executa uma consulta simples e chama **sqlsrv_free_stmt** para liberar todos os recursos associados à instrução. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM Person.Contact");  
if( $stmt )  
{  
     echo "Statement executed.\n";  
}  
else  
{  
     echo "Query could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*-------------------------------  
     Process query results here.  
-------------------------------*/  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  

[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)  
  
