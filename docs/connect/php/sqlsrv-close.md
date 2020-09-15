---
description: sqlsrv_close
title: sqlsrv_close | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_close
apitype: NA
helpviewer_keywords:
- sqlsrv_close
- API Reference, sqlsrv_close
ms.assetid: 6ac6209c-a134-4f8f-b88b-8eefaa1cbc7f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ef31416d2ac40677e5907c96290ec8e32845862
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414172"
---
# <a name="sqlsrv_close"></a>sqlsrv_close
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Fecha a conexão especificada e libera os recursos associados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_close( resource $conn )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: a conexão a ser fechada.  
  
## <a name="return-value"></a>Valor de retorno  
O valor booliano **true** , a menos que a função seja chamada com um parâmetro inválido. Se a função for chamada com um parâmetro inválido, **false** será retornado.  
  
> [!NOTE]  
> **Null** é um parâmetro válido para esta função. Isso permite que a função seja chamada várias vezes em um script. Por exemplo, se você fechar uma conexão em uma condição de erro e fechá-la novamente no final do script, a segunda chamada para **sqlsrv_close** retornará **true** porque a primeira chamada para **sqlsrv_close** (na condição de erro) define o recurso de conexão como **null**.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir fecha uma conexão. O exemplo supõe que o SQL Server esteja instalado no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
//-----------------------------------------------  
// Perform operations with connection here.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
echo "Connection closed.\n";  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
