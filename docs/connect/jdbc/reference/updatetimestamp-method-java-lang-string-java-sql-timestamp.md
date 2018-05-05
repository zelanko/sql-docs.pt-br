---
title: Método updateTimestamp (Java, Java.SQL. timestamp) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateTimestamp (java.lang.String, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6d468357-bf73-484c-9a30-3671e399cf26
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3bcc0d80dee621c5b0484749bf12cbfdbb33d126
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updatetimestamp-method-javalangstring-javasqltimestamp"></a>Método updateTimestamp (java.lang.String, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de carimbo de data/hora, considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateTimestamp(java.lang.String columnName,  
                            java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
 *x*  
  
 Um valor de carimbo de data/hora.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateTimestamp é especificado pelo método updateTimestamp na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateTimestamp &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
