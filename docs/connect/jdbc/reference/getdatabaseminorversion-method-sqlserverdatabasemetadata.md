---
title: Método getDatabaseMinorVersion (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getDatabaseMinorVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18163668-60d6-4d54-aaf1-c338b8c90f2a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab9641bd909f0922f577e1f889e410831b1d3ce7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getdatabaseminorversion-method-sqlserverdatabasemetadata"></a>Método getDatabaseMinorVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número da versão secundária do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getDatabaseMinorVersion()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica a versão secundária do banco de dados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getDatabaseMinorVersion é especificado pelo método getDatabaseMinorVersion na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
