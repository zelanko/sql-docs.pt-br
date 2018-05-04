---
title: Método nullsAreSortedHigh (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedHigh
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ff97d37-befc-47b1-8092-505917216a41
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f524c27b7dd6bccceb8357b1c10c1ee7822c438
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="nullsaresortedhigh-method-sqlserverdatabasemetadata"></a>Método nullsAreSortedHigh (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se os valores NULL são classificados de cima para baixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean nullsAreSortedHigh()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se os valores forem classificados como alto. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método nullsAreSortedHigh é especificado pelo método nullsAreSortedHigh na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
