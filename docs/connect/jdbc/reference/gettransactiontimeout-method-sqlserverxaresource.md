---
title: Método getTransactionTimeout (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.getTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed0a37e9-1132-4d3f-b88f-8be674e852b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7aa67a0d4cc8a218500d278783f9dc8b6026fb0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978618"
---
# <a name="gettransactiontimeout-method-sqlserverxaresource"></a>Método getTransactionTimeout (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém o valor de tempo limite da transação atual para o objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getTransactionTimeout()  
```  
  
## <a name="exceptions"></a>Exceções  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentários  
 Esse método getTransactionTimeout é especificado pelo método getTransactionTimeout na interface javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
