---
description: Método end (SQLServerXAResource)
title: Método end (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.end
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e6418b27-793b-4b36-8dfb-756aec7bcbba
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7908c25c3366903d13ac27c2cefbb349ef43b4b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437818"
---
# <a name="end-method-sqlserverxaresource"></a>Método end (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Termina o trabalho executado em nome de uma ramificação de transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void end(javax.transaction.xa.Xid xid,  
                int flags)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *xid*  
  
 Um objeto Xid.  
  
 *sinalizadores*  
  
 Um valor **int**.  
  
## <a name="exceptions"></a>Exceções  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentários  
 Esse método end é especificado pelo método end na interface javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
