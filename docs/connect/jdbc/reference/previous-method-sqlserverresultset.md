---
title: Método previous (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.previous
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66eb4e10-c375-4b31-ac46-3ba1d9dbf6a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1f13c3fedc3cfaa0645eec5a769ed482b339563
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976005"
---
# <a name="previous-method-sqlserverresultset"></a>Método previous (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor para a linha anterior no objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean previous()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se a nova linha atual for válida. **false** se não houver mais linhas a processar.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método previous é especificado pelo método previous na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
