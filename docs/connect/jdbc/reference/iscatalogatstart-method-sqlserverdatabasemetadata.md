---
title: Método isCatalogAtStart (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.isCatalogAtStart
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 665173d2-14c7-4ce1-954e-4adb53fb9b39
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e5f6211831e8c8b343b65814ce59848b3a1875e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="iscatalogatstart-method-sqlserverdatabasemetadata"></a>Método isCatalogAtStart (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se um catálogo aparece no início de um nome de tabela totalmente qualificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isCatalogAtStart()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se o nome de catálogo aparecer primeiro. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isCatalogAtStart é especificado pelo método isCatalogAtStart na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
