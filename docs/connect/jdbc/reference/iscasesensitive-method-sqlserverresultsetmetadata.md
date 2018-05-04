---
title: Método isCaseSensitive (SQLServerResultSetMetaData) | Microsoft Docs
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
- SQLServerResultSetMetaData.isCaseSensitive
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4db67eb7-7ff2-4fb8-8052-39f699de53ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d65c511e2cf49718f1e62a8afb0d6d8efc4c1cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="iscasesensitive-method-sqlserverresultsetmetadata"></a>Método isCaseSensitive (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se uma coluna diferencia maiúsculas de minúsculas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isCaseSensitive(int column)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *column*  
  
 Um **int** que indica o índice da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a coluna diferencia maiusculas de minúsculas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isCaseSensitive é especificado pelo método isCaseSensitive na interface Java.SQL. resultsetmetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros de SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
