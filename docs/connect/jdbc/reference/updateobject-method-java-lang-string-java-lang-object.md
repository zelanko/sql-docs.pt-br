---
title: Método updateObject (Java, java.lang.Object) | Microsoft Docs
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
- SQLServerResultSet.updateObject (java.lang.String, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6999d9c-eab6-4e4d-96d8-e0fa4b4b87e3
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cfb250d9cb00216f712f64407d607ad120b5188
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updateobject-method-javalangstring-javalangobject"></a>Método updateObject (java.lang.String, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um **objeto** valor, considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
 *obj*  
  
 Um **objeto** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateObject é especificado pelo método updateObject na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateObject &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
