---
title: sqlsrv_server_info | Microsoft Docs
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
- sqlsrv_server_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_server_info
- sqlsrv_server_info
ms.assetid: ef6fe2b7-d267-4379-b948-5626c4684367
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ca576d890d943aa7df98495ff8a18c91d11e0866
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvserverinfo"></a>sqlsrv_server_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna informações sobre o servidor. É necessário estabelecer uma conexão antes de chamar essa função.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_server_info( resource $conn)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: o recurso de conexão pelo qual o cliente e o servidor estão conectados.  
  
## <a name="return-value"></a>Valor de retorno  
Uma matriz associativa com as seguintes chaves:  
  
|Chave|Descrição|  
|-------|---------------|  
|CurrentDatabase|O banco de dados de destino no momento.|  
|SQLServerVersion|A versão do SQL Server.|  
|SQLServerName|O nome do servidor.|  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir grava informações do servidor no console quando o exemplo é executado na linha de comando.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$server_info = sqlsrv_server_info( $conn);  
if( $server_info )  
{  
      foreach( $server_info as $key => $value)  
      {  
             echo $key.": ".$value."\n";  
      }  
}  
else  
{  
      echo "Error in retrieving server info.\n";  
      die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)  
[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  

