---
title: Método supportsDataManipulationTransactionsOnly | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsDataManipulationTransactionsOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bdc182db-4518-4bf2-b63a-05f58fdb4eb8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afb5c598a00fe4aa3fb6405dfe7b7edd67f79f29
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654734"
---
# <a name="supportsdatamanipulationtransactionsonly-method-sqlserverdatabasemetadata"></a>Método supportsDataManipulationTransactionsOnly (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte somente a instruções de manipulação de dados em uma transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsDataManipulationTransactionsOnly()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsDataManipulationTransactionsOnly é especificado pelo método supportsDataManipulationTransactionsOnly na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
