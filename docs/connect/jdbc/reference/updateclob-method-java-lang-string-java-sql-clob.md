---
title: "Método updateClob (Java, CLOB) | Microsoft Docs"
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
- SQLServerResultSet.updateClob (java.lang.String, java.sql.Clob)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5da64915-1c13-44fd-90c0-52168889bae0
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ea8e31b6917758d79b492d571b6e96d3b382c603
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updateclob-method-javalangstring-javasqlclob"></a>Método updateClob (java.lang.String, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor java.sql.Clob considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateClob(java.lang.String columnName,  
                       java.sql.Clob clobValue)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
 *clobValue*  
  
 Um objeto Clob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateClob é especificado pelo método updateClob na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateClob &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

