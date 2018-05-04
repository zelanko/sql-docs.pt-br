---
title: Método (SQLServerResultSet) getConcurrency | Microsoft Docs
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
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38a9bf912c0a967a29c8a6ff3543418d1c29b957
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o modo de simultaneidade deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o tipo de simultaneidade, que pode ser um dos seguintes valores:  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getConcurrency é especificado pelo método getConcurrency na interface Java.SQL. resultset.  
  
 A simultaneidade usada é determinada pelo [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que criou o conjunto de resultados.  
  
 Esse método pode ser usado para determinar a simultaneidade real. Se o aplicativo selecionou CONCUR_READ_ONLY ou CONCUR_UPDATABLE, esses valores serão retornados. Se o aplicativo usou a simultaneidade padrão, o valor CONCUR_READ_ONLY será retornado.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
