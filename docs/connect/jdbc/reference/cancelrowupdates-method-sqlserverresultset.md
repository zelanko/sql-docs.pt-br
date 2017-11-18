---
title: "Método (SQLServerResultSet) cancelRowUpdates | Microsoft Docs"
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
- SQLServerResultSet.cancelRowUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ecacca4-f7bc-4f5d-886a-da7747fdccae
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3823cc47e56615b29f33f3f37e1178afe0094022
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="cancelrowupdates-method-sqlserverresultset"></a>cancelRowUpdates método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cancela as atualizações feitas na linha atual nesta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void cancelRowUpdates()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método cancelRowUpdates é especificado pelo método cancelRowUpdates na interface Java.SQL. resultset.  
  
 Esse método pode ser chamado depois de chamar um método updater e antes de chamar o [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) método para reverter as atualizações que foram feitas em uma linha. Se não há atualizações foram feitas ou updateRow já foi chamado, esse método não tem efeito.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

