---
title: Método Recover (SQLServerXAResource) | Microsoft Docs
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
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72efa07b757aaeab8a51646e802e8c5908a62d07
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="recover-method-sqlserverxaresource"></a>Método recover (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém uma lista de ramificações de transação preparadas de um gerenciador de recursos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *flags*  
  
 Um **int** valor que pode ter um dos seguintes valores: XAResource.TMSTARTRSCAN ou XAResource.TMENDRSCAN ou XAResource.TMNOFLAGS ou XAResource.TMSTARTTRSCAN | XAResource.TMENDRSCAN.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto Xid.  
  
## <a name="exceptions"></a>Exceções  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 Esse método de recuperação é especificado pelo método de recuperação na interface javax.  
  
 Se o parâmetro **sinalizador** não é XAResource.TMSTARTRSCAN ou XAResource.TMSTARTRSCAN | XAResource.TMENDRSCAN, um exame de recuperação deve estar em andamento.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
