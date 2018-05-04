---
title: Método (Java) (SQLServerResultSet) getSQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab9c7b10-026f-4a51-8d60-e6871d1abd02
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2aa202591cbfc2379df8cab44cfed55d80582104
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getsqlxml-method-javalangstring-sqlserverresultset"></a>Método getSQLXML (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor de uma coluna designada na linha atual do [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto SQLXML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que indica o rótulo da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 ASQLXMLobject.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getSQLXML é especificado pelo método getSQLXML na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método getSQLXML &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
