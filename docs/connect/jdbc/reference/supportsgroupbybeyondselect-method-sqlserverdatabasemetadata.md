---
title: Método supportsGroupByBeyondSelect (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsGroupByBeyondSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eadd2c37-d9ec-4b47-a91e-ed90b1eaf4b4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 610100e8a9634fd25232b515533d993bb459b2bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66788617"
---
# <a name="supportsgroupbybeyondselect-method-sqlserverdatabasemetadata"></a>Método supportsGroupByBeyondSelect (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte ao uso de colunas que não são incluídas na instrução SELECT em uma cláusula GROUP BY, contanto que sejam incluídas todas as colunas na instrução SELECT na cláusula GROUP BY.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsGroupByBeyondSelect()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsGroupByBeyondSelect é especificado pelo método supportsGroupByBeyondSelect na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
