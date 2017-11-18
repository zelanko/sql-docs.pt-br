---
title: "Método (Java, Java) getPooledConnection | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c62f975b9d9176941906f3ab8b5e5d7d241d14ff
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getpooledconnection-method-javalangstring-javalangstring"></a>Método getPooledConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta estabelecer uma conexão de banco de dados física que pode ser usada como uma conexão em pool com base no nome de usuário e senha fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.sql.PooledConnection getPooledConnection(java.lang.String user,  
                                                      java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *usuário*  
  
 Um **cadeia de caracteres** que contém o nome de usuário.  
  
 *passwword*  
  
 Um **cadeia de caracteres** que contém a senha.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método getPooledConnection é especificado pelo método getPooledConnection na interface javax.SQL. connectionpooldatasource.  
  
## <a name="see-also"></a>Consulte também  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [Métodos SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Membros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  

