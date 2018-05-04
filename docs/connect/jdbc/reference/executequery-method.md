---
title: Método executeQuery () | Microsoft Docs
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
- SQLServerPreparedStatement.executeQuery ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1d90407f-16df-4ba2-b4a5-47d5751e1d7c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3131002b9578ebd02a9f59850af3f7d5adf8e647
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executequery-method-"></a>Método executeQuery ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a consulta SQL no objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e retorna o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão gerado pela consulta.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet executeQuery()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método executeQuery é especificado pelo método executeQuery na interface PreparedStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método executeQuery &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
