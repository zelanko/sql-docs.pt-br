---
title: "Método (SQLServerStatement) getUpdateCount | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 50d702db72b2d02cc52401d76cd289a3b21de81a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>Comentários  
 Esse método getUpdateCount é especificado pelo método getUpdateCount na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
