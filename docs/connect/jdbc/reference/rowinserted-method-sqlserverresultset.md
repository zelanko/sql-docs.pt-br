---
title: Método (SQLServerResultSet) rowInserted | Microsoft Docs
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
- SQLServerResultSet.rowInserted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e7c10372-0be8-4baa-87f7-ed6b66003357
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 224ee6eef64da19c76ccc3d65aa32c91f1636119
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rowinserted-method-sqlserverresultset"></a>rowInserted método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se a linha atual teve uma inserção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean rowInserted()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se uma linha teve uma inserção e as inserções são detectadas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método rowUpdated é especificado pelo método rowUpdated na interface Java.SQL. resultset.  
  
 O valor retornado depende se isso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto detectar inserções visíveis.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] não detecta linhas inseridas para qualquer tipo de cursor.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
