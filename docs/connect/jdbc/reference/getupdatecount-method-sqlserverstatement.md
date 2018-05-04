---
title: Método (SQLServerStatement) getUpdateCount | Microsoft Docs
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
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ec60f62adb3be2752bf460d88460f5ce91b18ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getupdatecount-method-sqlserverstatement"></a>getUpdateCount método (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o resultado atual como uma contagem de atualização.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que contém a contagem de atualização. Se o resultado retornado for um objeto do conjunto de resultados ou não houver mais resultados, será retornado o valor -1.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getUpdateCount é especificado pelo método getUpdateCount na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
