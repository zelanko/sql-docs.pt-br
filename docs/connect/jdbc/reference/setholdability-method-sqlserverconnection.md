---
title: "Método (SQLServerConnection) setHoldability | Microsoft Docs"
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
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cfc1f5eb9b3c6368cfe0dd659146bcfa7353bf89
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setholdability-method-sqlserverconnection"></a>setHoldability método (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Altera a colocação em espera de [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que são criados usando esse [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto para a colocação em espera fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nNewHold*  
  
 Um **int** valor que contenha um dos seguintes níveis de suspensão:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setHoldability é especificado pelo método setHoldability na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
