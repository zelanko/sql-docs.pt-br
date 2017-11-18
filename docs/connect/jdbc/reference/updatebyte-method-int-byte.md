---
title: "Método updateByte (int, byte) | Microsoft Docs"
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
- SQLServerResultSet.updateByte (int, byte)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e635d789-9218-488e-a213-2e3e09635acc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 348642d7df7313a6336cb5a8bd05826ab6c814a4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updatebyte-method-int-byte"></a>Método updateByte (int, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um **bytes** valor, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateByte(int index,  
                       byte x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *índice*  
  
 Um **int** que indica o índice da coluna.  
  
 *x*  
  
 Um **bytes** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateByte é especificado pelo método updateByte na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateByte &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

