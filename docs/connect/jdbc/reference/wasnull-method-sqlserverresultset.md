---
title: "Método (SQLServerResultSet) wasNull | Microsoft Docs"
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
- SQLServerResultSet.wasNull
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d37f80ef-d72c-4429-ada3-1d685bdab6d7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1e787f37570e0475ca0f046b0d7302c7981fa0dd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="wasnull-method-sqlserverresultset"></a>wasNull método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Verifica se o último valor lido era nulo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean wasNull()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se o último valor lido era nulo. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método wasNull é especificado pelo método wasNull na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

