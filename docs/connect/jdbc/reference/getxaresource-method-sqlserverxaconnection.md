---
description: Método getXAResource (SQLServerXAConnection)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a523a1a1b731288632c969baee1170408734a81
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433698"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>Método getXAResource (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) que o gerenciador de transação usará para gerenciar a participação desse objeto [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) em uma transação distribuída.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto XAResource.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método getXAResource é especificado pelo método getXAResource na interface java.sql.XAConnection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [Membros SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Classe SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
