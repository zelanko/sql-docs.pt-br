---
title: Método supportsAlterTableWithDropColumn | Microsoft Docs
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
- SQLServerDatabaseMetaData.supportsAlterTableWithDropColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 55a182c1-28e5-4d32-aeb1-166a8ac76758
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a542e8454d4165dc593437a0abd3ede2581186e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supportsaltertablewithdropcolumn-method-sqlserverdatabasemetadata"></a>Método supportsAlterTableWithDropColumn (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte a ALTER TABLE com drop column.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsAlterTableWithDropColumn()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsAlterTableWithDropColumn é especificado pelo método supportsAlterTableWithDropColumn na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
