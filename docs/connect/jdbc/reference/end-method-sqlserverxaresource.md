---
title: Método end (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerXAResource.end
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e6418b27-793b-4b36-8dfb-756aec7bcbba
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a65198a91bff995e98479b396a87fd11baefe38f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 *XID*  
  
 Um objeto Xid.  
  
 *flags*  
  
 Um **int** valor.  
  
## <a name="exceptions"></a>Exceções  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 Esse método final é especificado pelo método final na interface javax.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
