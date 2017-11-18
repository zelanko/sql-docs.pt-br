---
title: "Método isSameRM (SQLServerXAResource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerXAResource.isSameRM
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa24c46-b7cf-470a-afa1-52301847a448
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27cc769b71dffcb47c1575c73c778fbd43e73656
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="issamerm-method-sqlserverxaresource"></a>Método isSameRM (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Determina se a instância do Gerenciador de recursos que é representada pelo objeto de destino é o mesmo que a instância do Gerenciador de recursos que é representada pelo objeto XAResource fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isSameRM(javax.transaction.xa.XAResource xares)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *xares*  
  
 Um objeto de XAResource.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se as instâncias são iguais. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentários  
 Esse método de confirmação é especificado pelo método na interface javax confirmação.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  

