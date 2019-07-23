---
title: Método supportsPositionedDelete (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsPositionedDelete
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8011659a-d74b-489b-a88b-08bd9e8b48b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1dbe35f0d0068cabd92f3f8ff538e15fc0b81668
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969026"
---
# <a name="supportspositioneddelete-method-sqlserverdatabasemetadata"></a>Método supportsPositionedDelete (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte a instruções DELETE posicionadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsPositionedDelete()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsPositionedDelete é especificado pelo método supportsPositionedDelete na interface java. Sql. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
