---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d0d59186e15dc07d1d4e91ac673c456ec592d01
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67952821"
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
  
  
