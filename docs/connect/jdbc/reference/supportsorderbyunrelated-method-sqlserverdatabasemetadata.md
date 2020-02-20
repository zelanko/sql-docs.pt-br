---
title: Método supportsOrderByUnrelated (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOrderByUnrelated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9ea6c534-8132-49f3-aac3-a12ec4c46df2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ddbb8fa811a4370db06b4992eb43e26845e1298
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969076"
---
# <a name="supportsorderbyunrelated-method-sqlserverdatabasemetadata"></a>Método supportsOrderByUnrelated (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte ao uso de uma coluna que não está na instrução SELECT em uma cláusula ORDER BY.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsOrderByUnrelated()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método supportsOrderByUnrelated é especificado pelo método supportsOrderByUnrelated na interface java.Sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
