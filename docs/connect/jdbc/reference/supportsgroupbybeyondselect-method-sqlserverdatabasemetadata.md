---
title: Método supportsGroupByBeyondSelect (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.supportsGroupByBeyondSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eadd2c37-d9ec-4b47-a91e-ed90b1eaf4b4
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e92b7b164ac0321173aaa65744dc16afe4792a92
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supportsgroupbybeyondselect-method-sqlserverdatabasemetadata"></a>Método supportsGroupByBeyondSelect (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte ao uso de colunas que não são incluídas na instrução SELECT em uma cláusula GROUP BY, contanto que sejam incluídas todas as colunas na instrução SELECT na cláusula GROUP BY.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsGroupByBeyondSelect()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsGroupByBeyondSelect é especificado pelo método supportsGroupByBeyondSelect na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
