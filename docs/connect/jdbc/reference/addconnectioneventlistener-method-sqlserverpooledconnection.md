---
title: Método addConnectionEventListener (SQLServerPooledConnection) | Microsoft Docs
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
- SQLServerPooledConnection.addConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 142830a8-8d4e-48ca-911d-85bf195ca4fe
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d927a6e9ae0bbbf7008f2177e0f3411ad8a43747
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>Método addConnectionEventListener (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra o ouvinte de evento fornecido para que ele seja notificado quando ocorre um evento neste [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Ouvinte*  
  
 Um objeto ConnectionEventListener.  
  
## <a name="remarks"></a>Remarks  
 Esse método addConnectionEventListener é especificado pelo método addConnectionEventListener na interface javax.SQL. pooledconnection.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [Membros SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [Classe SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
