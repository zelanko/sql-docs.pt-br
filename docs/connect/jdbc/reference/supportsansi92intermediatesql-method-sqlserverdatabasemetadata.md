---
title: Método supportsANSI92IntermediateSQL (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsANSI92IntermediateSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d6e8301-0633-4565-91c6-a80910954461
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fab9580485a4eab7ebb4967b4f8461c7dbc098e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969790"
---
# <a name="supportsansi92intermediatesql-method-sqlserverdatabasemetadata"></a>Método supportsANSI92IntermediateSQL (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se este banco de dados oferece suporte à gramática de SQL intermediária do padrão ANSI92.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsANSI92IntermediateSQL()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsANSI92IntermediateSQL é especificado pelo método supportsANSI92IntermediateSQL na interface java. Sql. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
