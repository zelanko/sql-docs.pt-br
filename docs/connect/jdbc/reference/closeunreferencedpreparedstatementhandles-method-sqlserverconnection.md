---
description: Método closeUnreferencedPreparedStatementHandles (SQLServerConnection)
title: Método closeUnreferencedPreparedStatementHandles (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.closeUnreferencedPreparedStatementHandles
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62b49401f5c2fe04b997aba1d669ea96ebb826fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438078"
---
# <a name="closeunreferencedpreparedstatementhandles-method-sqlserverconnection"></a>Método closeUnreferencedPreparedStatementHandles (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Força o cancelamento da preparação das solicitações para as instruções preparadas descartadas pendentes a serem executadas.

## <a name="syntax"></a>Sintaxe  
  
```  
  
public void closeUnreferencedPreparedStatementHandles()  
```  


## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  

## <a name="remarks"></a>Comentários  
 Esse método está disponível no driver JDBC versão 6.4 e posteriores.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
