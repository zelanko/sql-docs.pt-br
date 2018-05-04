---
title: Método getPooledConnection () | Microsoft Docs
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
- SQLServerConnectionPoolDataSource.getPooledConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aad6c325-3398-462c-aa6e-201dc89fa5ef
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f94e8fe64c451ad8e7985169236c6d10e9b3572
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getpooledconnection-method-"></a>Método getPooledConnection ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta estabelecer uma conexão de banco de dados física que possa ser usada como uma conexão em pool.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.sql.PooledConnection getPooledConnection()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método getPooledConnection é especificado pelo método getPooledConnection na interface javax.SQL. connectionpooldatasource.  
  
## <a name="see-also"></a>Consulte também  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [Métodos SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Membros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
