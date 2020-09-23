---
title: sqlsrv_client_info
description: A referência de API da função sqlsrv_errors no Driver SQLSRV da Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_client_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_client_info
- sqlsrv_client_info
ms.assetid: 3e2d3679-436a-45d8-8bdc-7c633b65a720
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d1ebcbe7a022d438e1e7e10c42098127496c1f7
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411182"
---
# <a name="sqlsrv_client_info"></a>sqlsrv_client_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna informações sobre a conexão e a pilha do cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_client_info( resource $conn)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: o recurso de conexão pelo qual o cliente está conectado.  
  
## <a name="return-value"></a>Valor de retorno  
Uma matriz associativa com chaves descritas na tabela abaixo, ou **false** , se o recurso de conexão for nulo.  
  
**Para versões 3.2 e 3.1 do PHP para SQL Server**:  
  
|Chave|Descrição|  
|-------|---------------|  
|DriverDllName|MSODBCSQL11.DLL (ODBC Driver 11 for SQL Server)|  
|DriverODBCVer|Versão do ODBC (xx.yy)|  
|DriverVer|Versão do ODBC Driver 11 for SQL Server:<br /><br />xx.yy.zzzz ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 3.2 ou 3.1)|  
|ExtensionVer|versão do php_sqlsrv.dll:<br /><br />3.2.xxxx.x (para [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 3.2)<br /><br />3.1.xxxx.x (para [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 3.1)|  
  
**Para versões 3.0 e 2.0 do PHP para SQL Server**:  
  
|Chave|Descrição|  
|-------|---------------|  
|DriverDllName|SQLNCLI10.DLL ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 2.0)|  
|DriverODBCVer|Versão do ODBC (xx.yy)|  
|DriverVer|Versão de DLL do SQL Server Native Client:<br /><br />10.50.xxx ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 2.0)|  
|ExtensionVer|versão do php_sqlsrv.dll:<br /><br />2.0.xxxx.x ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versão 2.0)|  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir grava informações do cliente no console quando o exemplo é executado na linha de comando. O exemplo supõe que o SQL Server esteja instalado no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
if( $client_info = sqlsrv_client_info( $conn))  
{  
       foreach( $client_info as $key => $value)  
      {  
              echo $key.": ".$value."\n";  
      }  
}  
else  
{  
       echo "Client info error.\n";  
}  
  
/* Close connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
