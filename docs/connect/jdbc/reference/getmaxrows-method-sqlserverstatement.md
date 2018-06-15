---
title: Método (SQLServerStatement) getMaxRows | Microsoft Docs
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
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d619f9505d9f6f5e9c2c6db7751ecb224fa2f5e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32835631"
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
  
  
