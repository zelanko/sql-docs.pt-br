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
ms.openlocfilehash: 0f2e6148572d6ec6c7e9b52a704d79e8a9124ccf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977885"
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
  
## <a name="remarks"></a>Comentários  
 Esse método insertRow é especificado pelo método insertRow na interface java.sql.ResultSet.  
  
 O cursor deve estar na linha inserida quando esse método for chamado. Depois do método ser chamado, o cursor permanecerá na linha inserida e o conjunto de resultados permanecerá no modo de inserção.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
