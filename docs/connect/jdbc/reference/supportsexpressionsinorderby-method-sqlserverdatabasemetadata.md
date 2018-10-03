---
title: Método supportsExpressionsInOrderBy (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsExpressionsInOrderBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 858f3c02-4531-4775-97e9-a03b316bdaba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 249e10054a537ed26006551a6f8b09b05f741ac3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721004"
---
# <a name="supportsexpressionsinorderby-method-sqlserverdatabasemetadata"></a>Método supportsExpressionsInOrderBy (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte a expressões em listas ORDER BY.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsExpressionsInOrderBy()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsExpressionsInOrderBy é especificado pelo método supportsExpressionsInOrderBy na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
