---
title: "Método addConnectionEventListener (SQLServerPooledConnection) | Microsoft Docs"
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
- SQLServerPooledConnection.addConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 142830a8-8d4e-48ca-911d-85bf195ca4fe
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0054071b9fe6ddc814d0973de3af3adbaaa228e0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>Método addConnectionEventListener (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra o ouvinte de evento fornecido para que ele seja notificado quando ocorre um evento neste [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ouvinte*  
  
 Um objeto ConnectionEventListener.  
  
## <a name="remarks"></a>Comentários  
 Esse método addConnectionEventListener é especificado pelo método addConnectionEventListener na interface javax.SQL. pooledconnection.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [Membros SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [Classe SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  

