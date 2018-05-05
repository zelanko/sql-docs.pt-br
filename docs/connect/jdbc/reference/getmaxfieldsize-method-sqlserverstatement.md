---
title: Método (SQLServerStatement) getMaxFieldSize | Microsoft Docs
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
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d98c7ec1ba9b814f17e3c401eb9a55aa53f9ed46
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize método (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de bytes que podem ser retornadas para caracteres e valores de coluna binária em um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto que é produzido por esse [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número máximo de bytes que uma coluna pode conter ou 0 se não houver nenhum limite.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMaxFieldSize é especificado pelo método getMaxFieldSize na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
