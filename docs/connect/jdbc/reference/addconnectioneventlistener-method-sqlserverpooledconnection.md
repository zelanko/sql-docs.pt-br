---
title: Método addConnectionEventListener (SQLServerPooledConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPooledConnection.addConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 142830a8-8d4e-48ca-911d-85bf195ca4fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3481ae6f7a6c257c3fd438b4166339cf9507f136
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922980"
---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>Método addConnectionEventListener (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra o ouvinte de evento fornecido de forma que ele seja notificado quando um evento ocorrer no objeto [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *listener*  
  
 Um objeto ConnectionEventListener.  
  
## <a name="remarks"></a>Comentários  
 Esse método addConnectionEventListener é especificado pelo método addConnectionEventListener na interface javax.sql.PooledConnection.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [Membros SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [Classe SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
