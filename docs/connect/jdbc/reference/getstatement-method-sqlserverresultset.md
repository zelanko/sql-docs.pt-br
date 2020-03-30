---
title: Método getStatement (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7dea981b-b4fd-4f8d-954f-e686124627e2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c7fca859273c5eff58cde02b98f98699307ff1b4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979585"
---
# <a name="getstatement-method-sqlserverresultset"></a>Método getStatement (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que produziu o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Statement getStatement()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto SQLServerStatement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getStatement é especificado pelo método getStatement na interface java.sql.ResultSet.  
  
 Se o conjunto de resultados foi gerado de algum outro modo, como por um método [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), esse método retornará nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
