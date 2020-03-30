---
title: Método getTransactionIsolation (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 179772e9-6572-4ce5-83c5-ab2b196cee67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4b9a8b537e110f220203c0cda7d3ea27e8a6385e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978675"
---
# <a name="gettransactionisolation-method-sqlserverconnection"></a>Método getTransactionIsolation (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o nível de isolamento de transação atual do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getTransactionIsolation()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **int** que contém um dos seguintes níveis de isolamento:  
  
 TRANSACTION_NONE  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTransactionIsolation é especificado pelo método getTransactionIsolation na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
