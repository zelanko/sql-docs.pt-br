---
title: Método getSQLStateType (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aa0243e8b990783bfca96b769d4011cc6611f7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>Método getSQLStateType (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o SQLSTATE retornado pelo método SQLException.getSQLState é X/Open (agora conhecido como Open Group), SQL CLI, SQL99 (JDBC 3.0) ou SQL:2003 (JDBC 4.0).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o tipo de SQLSTATE que pode ser um dos seguintes valores:  
  
-   Para o Java Runtime Environment versão 5.0: se o **xopenStates** conexão está definida como **true**, esse método retorna DatabaseMetaData.sqlStateXOpen. Caso contrário, DatabaseMetaData.sqlStateSQL99.  
  
-   Para o Java Runtime Environment versão 6.0: se o **xopenStates** conexão está definida como **true**, esse método retorna DatabaseMetaData.sqlStateXOpen. Caso contrário, DatabaseMetaData.sqlStateSQL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getSQLStateType é especificado pelo método getSQLStateType na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
