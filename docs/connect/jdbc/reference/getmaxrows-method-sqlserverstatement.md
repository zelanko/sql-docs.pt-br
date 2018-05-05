---
title: Método (SQLServerStatement) getMaxRows | Microsoft Docs
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
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1f1b3fb36ca55635f8c038b3e6d327b7127a6af4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows método (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de linhas que uma [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto que é produzido por esse [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto pode conter.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número máximo de linhas ou 0 se não houver nenhum limite.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMaxRows é especificado pelo método getMaxRows na interface Java.SQL. Statement.  
  
 Esse método getMaxRows sempre retorna 0 para cursores roláveis dinâmicos.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
