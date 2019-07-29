---
title: Método isClosed (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6081aa34-fc88-4dd0-9a3f-05e8488219dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa1f768e79da36ce681b4096c64e5d46e21f5461
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977745"
---
# <a name="isclosed-method-sqlserverresultset"></a>Método isClosed (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) foi fechado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se esse objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) for fechado, **false** se ele ainda estiver aberto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isClosed é especificado pelo método isClosed na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
