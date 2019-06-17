---
title: Método getXAResource (SQLServerXAConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cbad0cdd9fe26c780e3acc5691f9af56e63ce1fe
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801771"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>Método getXAResource (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) que o gerenciador de transação usará para gerenciar a participação desse objeto [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) em uma transação distribuída.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto de XAResource.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método getXAResource é especificado pelo método getXAResource na interface xaconnection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [Membros SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Classe SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
