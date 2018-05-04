---
title: Método (Java) (SQLServerResultSet) getFloat | Microsoft Docs
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
- SQLServerResultSet.getFloat (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 09491a8a-1931-411e-9b35-2b269c1b7f12
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12f4b2b3c39a17c3c9e3e10c88d7c17161304b9e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getfloat-method-javalangstring-sqlserverresultset"></a>getFloat método (Java) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **float** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public float getFloat(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **float** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getFloat é especificado pelo método getFloat na interface Java.SQL. resultset.  
  
 Esse método retorna todos os tipos baseados em número com Java **float** fidelidade.  
  
## <a name="see-also"></a>Consulte também  
 [Método getFloat &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
