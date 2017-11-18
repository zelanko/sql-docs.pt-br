---
title: "Método (Java) (SQLServerResultSet) getDouble | Microsoft Docs"
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
- SQLServerResultSet.getDouble (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3ee26412-43d2-404b-bc05-ffd0fc75805c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ebe750b3bf20da6154d03f292c158596dde2d1dd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getdouble-method-javalangstring-sqlserverresultset"></a>getDouble método (Java) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **duplo** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public double getDouble(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **duplo** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getDouble é especificado pelo método getDouble na interface Java.SQL. resultset.  
  
 Este método retorna todos os tipos de dados com base em número com Java **duplo** fidelidade.  
  
## <a name="see-also"></a>Consulte também  
 [Método getDouble &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

