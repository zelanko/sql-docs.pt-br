---
title: Método getSQLStateType (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 55079e30c2f8908153cc708aca699e77aef41261
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66774181"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>Método getSQLStateType (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o SQLSTATE retornado pelo método SQLException.getSQLState é X/Open (agora conhecido como Open Group), SQL CLI, SQL99 (JDBC 3.0) ou SQL:2003 (JDBC 4.0).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o tipo de SQLSTATE que pode ter um dos seguintes valores:  
  
-   Para o Java Runtime Environment versão 5.0: se o **xopenStates** propriedade de conexão é definida como **verdadeiro**, esse método retornará DatabaseMetaData.sqlStateXOpen. Caso contrário, DatabaseMetaData.sqlStateSQL99.  
  
-   Para o Java Runtime Environment versão 6.0: se o **xopenStates** propriedade de conexão é definida como **verdadeiro**, esse método retornará DatabaseMetaData.sqlStateXOpen. Caso contrário, DatabaseMetaData.sqlStateSQL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getSQLStateType é especificado pelo método getSQLStateType na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
