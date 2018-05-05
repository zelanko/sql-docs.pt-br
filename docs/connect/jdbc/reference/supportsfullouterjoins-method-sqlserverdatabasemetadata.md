---
title: Método supportsFullOuterJoins (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsFullOuterJoins
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 836f1f45-59ed-4a34-9809-2000d3062576
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36d3c2a2173c6d6aa4096bed554ba06111b1c495
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supportsfullouterjoins-method-sqlserverdatabasemetadata"></a>Método supportsFullOuterJoins (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte a junções externas aninhadas completas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsFullOuterJoins()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsFullOuterJoins é especificado pelo método supportsFullOuterJoins na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
