---
title: Método (SQLServerResultSet) insertRow | Microsoft Docs
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
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eafc73e9a5a5179992cec3d042f82ac460ee2bd3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Adiciona o conteúdo da linha de inserção a este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto e no banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método insertRow é especificado pelo método insertRow na interface Java.SQL. resultset.  
  
 O cursor deve estar na linha inserida quando esse método for chamado. Depois do método ser chamado, o cursor permanecerá na linha inserida e o conjunto de resultados permanecerá no modo de inserção.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
