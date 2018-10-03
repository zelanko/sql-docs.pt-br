---
title: Método getStatementPoolingCacheSize (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 911137407c75d82164bf1ddd96eae91f618bb00b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841524"
---
# <a name="getstatementpoolingcachesize-method-sqlserverconnection"></a>Método getStatementPoolingCacheSize (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Retorna o tamanho do cache de instrução preparada para essa conexão. '0' significa que o cache não está habilitado.

## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getStatementPoolingCacheSize()  
```  

## <a name="return-value"></a>Valor retornado
 Uma **int** que contém o valor de **statementPoolingCacheSize** propriedade de conexão.

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método está disponível na versão do JDBC driver 6.4 e daí.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
