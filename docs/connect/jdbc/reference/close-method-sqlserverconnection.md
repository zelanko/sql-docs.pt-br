---
title: "Feche o método (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f0f26585-bdf7-4737-b434-8c7e115c8e94
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9f7dc84edb37bde6242be79830198ab565547e0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="close-method-sqlserverconnection"></a>Feche o método (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Libera isso [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) do objeto banco de dados e recursos do JDBC imediatamente em vez de aguardar que eles sejam liberados automaticamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método fechar é especificado pelo método Fechar na interface Java.SQL.  
  
 Chamar o método close no meio de uma transação faz com que a transação ser revertida.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

