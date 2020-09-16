---
description: Método getConcurrency (SQLServerResultSet)
title: Método getConcurrency (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8cb92a019c9c65e867be023fab9bc299a7a8bc8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436548"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>Método getConcurrency (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o modo de simultaneidade do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o tipo de simultaneidade, que pode ter um dos seguintes valores:  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getConcurrency é especificado pelo método getConcurrency na interface java.sql.ResultSet.  
  
 A simultaneidade usada é determinada pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que criou o conjunto de resultados.  
  
 Esse método pode ser usado para determinar a simultaneidade real. Se o aplicativo selecionou CONCUR_READ_ONLY ou CONCUR_UPDATABLE, esses valores serão retornados. Se o aplicativo usou a simultaneidade padrão, o valor CONCUR_READ_ONLY será retornado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
