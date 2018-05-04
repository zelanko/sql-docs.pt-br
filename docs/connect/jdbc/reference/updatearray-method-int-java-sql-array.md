---
title: Método updateArray (int, Java.SQL. Array) | Microsoft Docs
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
apiname:
- SQLServerResultSet.updateArray (int, java.sql.Array)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 464f7e3f-3e8a-4b2d-aebd-1c040583d52c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7238734bd32625f237df5eda7e95e8397aa5129c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updatearray-method-int-javasqlarray"></a>Método updateArray (int, java.sql.Array)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um objeto de matriz, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateArray(int columnIndex,  
                        java.sql.Array x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
 *x*  
  
 Um objeto de matriz.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateArray é especificado pelo método updateArray na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateArray &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
