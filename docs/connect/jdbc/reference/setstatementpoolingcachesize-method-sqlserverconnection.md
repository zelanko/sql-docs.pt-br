---
title: setStatementPoolingCacheSize método (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.setStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6084638ff0e5a7fff6bf6026d2a0b37c396400b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setstatementpoolingcachesize-method-sqlserverconnection"></a>setStatementPoolingCacheSize método (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Define o tamanho do cache de instrução preparada para esta conexão. Funciona se disableStatementPooling for definido como false e o valor > 0.

## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setStatementPoolingCacheSize(int statementPoolingCacheSize)  
```  

#### <a name="parameters"></a>Parâmetros  
 *statementPoolingCacheSize*  
  
 O novo valor da **statementPoolingCacheSize** propriedade de conexão.  

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
