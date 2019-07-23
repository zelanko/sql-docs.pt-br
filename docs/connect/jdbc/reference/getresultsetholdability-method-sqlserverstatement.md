---
title: Método getResultSetHoldability (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 053549ee-2018-47ab-9538-789dac2b150a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 153da54f0b70d94b4428e2152db6b159230fa38c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980318"
---
# <a name="getresultsetholdability-method-sqlserverstatement"></a>Método getResultSetHoldability (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a suspensão do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getResultSetHoldability()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica a suspensão do conjunto de resultados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getResultSetHoldability é especificado pelo método getResultSetHoldability na interface java. Sql. Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
