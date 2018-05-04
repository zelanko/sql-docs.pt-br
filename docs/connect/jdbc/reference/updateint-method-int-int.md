---
title: Método updateInt (int, int) | Microsoft Docs
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
- SQLServerResultSet.updateInt (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f4f651b0-a822-4bd4-b391-cc2355154a2a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9834e460d6b5ed7296480e51496617126094efdb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updateint-method-int-int"></a>Método updateInt (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um **int** valor, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateInt(int index,  
                      int x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o índice da coluna.  
  
 *x*  
  
 Um **int** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateInt é especificado pelo método updateInt na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateInt &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
