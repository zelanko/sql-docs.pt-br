---
title: Método nullsAreSortedLow (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedLow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 30c06a9d-3513-42d0-8b2a-5a20ac31eb0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2259a68458b6ec1d82019bec7167ca167aa99d9e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976639"
---
# <a name="nullsaresortedlow-method-sqlserverdatabasemetadata"></a>Método nullsAreSortedLow (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se os valores NULL são classificados de baixo para cima.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean nullsAreSortedLow()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se os valores forem classificados como baixos. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método nullsAreSortedLow é especificado pelo método nullsAreSortedLow na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
