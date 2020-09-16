---
description: Método isClosed (SQLServerConnection)
title: Método isClosed (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d4a5e3c1d3634e52fd9b2d8244262c40fada06
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433588"
---
# <a name="isclosed-method-sqlserverconnection"></a>Método isClosed (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão foi fechado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se a conexão estiver fechada, **false** se não estiver.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método isClosed é especificado pelo método isClosed na interface java.sql.Connection.  
  
 Verifica o estado do objeto SQLServerConnection chamado. Uma conexão será fechada se o método [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) for chamado nela ou se alguns erros fatais ocorrerem. Esse método só retornará **true** quando for chamado depois que o método close tiver sido chamado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
