---
title: Método (SQLServerConnection) setTransactionIsolation | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd1a4fb0ef1c55c54a17dfe1825fd208ebd6035f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="settransactionisolation-method-sqlserverconnection"></a>setTransactionIsolation método (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta alterar o nível de isolamento da transação para esse [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto para um dado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTransactionIsolation(int level)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nível*  
  
 Um **int** valor que contenha um dos seguintes níveis de isolamento:  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setTransactionIsolation é especificado pelo método setTransactionIsolation na interface Java.SQL.  
  
 As transações não serão confirmadas se esse método for chamado no meio de uma transação.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
