---
title: Método prepareCall (Java, int, int) | Microsoft Docs
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
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2ca7aef5cf2f56693cffd239ea61c208b53cdf3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="preparecall-method-javalangstring-int-int"></a>Método prepareCall (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) objeto que gera [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos com o tipo e simultaneidade fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sql*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
 *resultSetType*  
  
 Um **int** que indica o tipo de conjunto de resultado.  
  
 *resultSetConcurrency*  
  
 Um **int** que indica o conjunto de resultados tipo de simultaneidade.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto CallableStatement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método prepareCall é especificado pelo método prepareCall na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Método prepareCall &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
