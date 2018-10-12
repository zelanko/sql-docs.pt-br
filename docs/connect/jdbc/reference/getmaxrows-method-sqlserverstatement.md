---
title: Método getMaxRows (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8cb1c317930d97263038d09bd84e8836d5f6f4ff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773634"
---
# <a name="getmaxrows-method-sqlserverstatement"></a>Método getMaxRows (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de linhas que um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) produzido pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) pode conter.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número máximo de linhas ou 0 se não houver limite.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMaxRows é especificado pelo método getMaxRows na interface Statement.  
  
 Esse método getMaxRows sempre retorna 0 para cursores roláveis dinâmicos.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
