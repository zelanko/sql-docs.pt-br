---
title: Método (SQLServerPreparedStatement) getParameterMetaData | Microsoft Docs
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
- SQLServerPreparedStatement.getParameterMetaData
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c2876dec-ce29-4b61-9d74-ec3173b8cba5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc0ffe500b818f657068e2b9380f4e3bc8542ab2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getparametermetadata-method-sqlserverpreparedstatement"></a>getParameterMetaData método (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número, tipos e propriedades dos parâmetros desse [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.sql.ParameterMetaData getParameterMetaData()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getParameterMetaData é especificado pelo método getParameterMetaData na interface PreparedStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
