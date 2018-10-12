---
title: Método getFetchDirection (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd40f1a3bc218093f8a34215d15291bd152310be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726114"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>Método getFetchDirection (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a direção de busca do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica a direção de busca atual.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getFetchDirection é especificado pelo método getFetchDirection na interface do resultset.  
  
 Esse método retornará FETCH_FORWARD para cursores de somente encaminhamento, a última configuração feita por uma chamada ao método [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) para outros tipos de cursor e FETCH_UNKNOWN para esses tipos de cursor se o método setFetchDirection nunca foi chamado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
