---
title: Método (SQLServerConnection) getTransactionIsolation | Microsoft Docs
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
- SQLServerConnection.getTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 179772e9-6572-4ce5-83c5-ab2b196cee67
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58c373095c63f3cd13294b7c472bea741e71b55c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="gettransactionisolation-method-sqlserverconnection"></a>Método (SQLServerConnection) getTransactionIsolation
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o nível de isolamento da transação atual deste [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getTransactionIsolation()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** valor que contenha um dos seguintes níveis de isolamento:  
  
 TRANSACTION_NONE  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTransactionIsolation é especificado pelo método getTransactionIsolation na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
