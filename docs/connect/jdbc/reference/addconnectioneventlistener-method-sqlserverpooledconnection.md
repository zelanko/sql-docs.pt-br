---
description: Método addConnectionEventListener (SQLServerPooledConnection)
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
ms.openlocfilehash: f0fbbcfd24d4dee568745f727c027d5ea8fda0d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438238"
---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>Método addConnectionEventListener (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra o ouvinte de evento fornecido de forma que ele seja notificado quando um evento ocorrer no objeto [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *listener*  
  
 Um objeto ConnectionEventListener.  
  
## <a name="remarks"></a>Comentários  
 Esse método addConnectionEventListener é especificado pelo método addConnectionEventListener na interface javax.sql.PooledConnection.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [Membros SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [Classe SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
