---
title: Método (Java) (SQLServerResultSet) getBlob | Microsoft Docs
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
- SQLServerResultSet.getBlob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9f730d45-b54a-4961-950e-f4447f7225e1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a90617bacdb894ce6b532951159cbc6b211225fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getblob-method-javalangstring-sqlserverresultset"></a>getBlob método (Java) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto de Blob na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Blob getBlob(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ColName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de Blob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBlob é especificado pelo método getBlob na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método getBlob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
