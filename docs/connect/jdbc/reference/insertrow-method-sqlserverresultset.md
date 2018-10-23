---
title: Método insertRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 611ba86c25f78cda15fcac53d8f31311d88e4840
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696865"
---
# <a name="insertrow-method-sqlserverresultset"></a>Método insertRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Adiciona o conteúdo da linha de inserção neste objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) e no banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método insertRow é especificado pelo método insertRow na interface do resultset.  
  
 O cursor deve estar na linha inserida quando esse método for chamado. Depois do método ser chamado, o cursor permanecerá na linha inserida e o conjunto de resultados permanecerá no modo de inserção.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
