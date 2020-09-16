---
description: Método nullsAreSortedHigh (SQLServerDatabaseMetaData)
title: Método nullsAreSortedHigh (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedHigh
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ff97d37-befc-47b1-8092-505917216a41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c01f0b05e62a6c7df268dbc76fb7aaa7bf2cfde4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433138"
---
# <a name="nullsaresortedhigh-method-sqlserverdatabasemetadata"></a>Método nullsAreSortedHigh (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se os valores NULL são classificados de cima para baixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean nullsAreSortedHigh()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se os valores forem classificados como altos. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método nullsAreSortedHigh é especificado pelo método nullsAreSortedHigh na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
