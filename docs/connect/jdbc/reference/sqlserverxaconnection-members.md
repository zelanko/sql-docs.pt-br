---
title: Membros SQLServerXAConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 188140965c0040f8454156555b71adbd2fe89ce9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxaconnection-members"></a>Membros SQLServerXAConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pelo [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) classe.  
  
## <a name="constructors"></a>Construtores  
 Nenhuma.  
  
## <a name="fields"></a>Campos  
 Nenhuma.  
  
## <a name="inherited-fields"></a>Campos herdados  
 Nenhuma.  
  
## <a name="methods"></a>Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|(Herdado de [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) registra o ouvinte de evento fornecido para que ele seja notificado quando ocorre um evento neste objeto de Conexão.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|(Herdado de [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) fecha a conexão física que representa esse objeto de Conexão.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|(Herdado de [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) cria um identificador de objeto para a conexão física que representa esse objeto de Conexão.|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|Recupera um [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) do objeto que o Gerenciador de transações usará para gerenciar a participação desse [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) objeto em uma transação distribuída.|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|(Herdado de [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) remove o ouvinte de evento fornecido.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|javax.sql.PooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
  
## <a name="see-also"></a>Consulte também  
 [Classe SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
