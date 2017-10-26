---
title: "Método (Java) executeQuery | Microsoft Docs"
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
- SQLServerPreparedStatement.executeQuery (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 610205c2-6bcd-426c-ad6f-9682551efdec
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ad4fe32e78984773325df4f34b3762f61a9924d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="executequery-method-javalangstring"></a>Método executeQuery (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida e retorna um único [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *SQL*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeQuery é especificado pelo método executeQuery na interface Java.SQL. Statement.  
  
 Esse método substitui o [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) que se encontra no método o [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe.  
  
 Chamar esse método resultará em uma exceção porque a instrução SQL para o objeto SQLServerPreparedStatement for especificada quando o objeto é criado.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) é gerada se a instrução SQL fornecida produz algo diferente de um único [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Método executeQuery &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

