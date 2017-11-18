---
title: "Método updateArray (Java, Java.SQL. Array) | Microsoft Docs"
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
- SQLServerResultSet.updateArray (java.lang.String, java.sql.Array)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6f2ced5a-1c7d-439a-aaa5-472b9f4fdeab
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dee3ee7b1669e84cb3a9d1bc9010f7245667c4d9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updatearray-method-javalangstring-javasqlarray"></a>Método updateArray (java.lang.String, java.sql.Array)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um objeto de matriz, considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateArray(java.lang.String columnName,  
                        java.sql.Array x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
 *x*  
  
 Um objeto de matriz.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateArray é especificado pelo método updateArray na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateArray &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

