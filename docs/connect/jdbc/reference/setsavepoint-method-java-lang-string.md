---
title: Método (Java) setSavepoint | Microsoft Docs
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
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 27e8f14b96b7b0f95e5134703d9fd480ae778e1f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setsavepoint-method-javalangstring"></a>Método setSavepoint (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um ponto de salvamento com o nome fornecido na transação atual e retorna o novo [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto que o representa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sName*  
  
 Um **cadeia de caracteres** valor que contém o nome do ponto de salvamento.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de ponto de salvamento.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setSavePoint é especificado pelo método setSavePoint na interface Java.SQL.  
  
 O *sName* argumento é escapado automaticamente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Método setSavepoint &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
