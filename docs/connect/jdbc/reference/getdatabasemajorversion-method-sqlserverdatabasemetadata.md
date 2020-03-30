---
title: Método getDatabaseMajorVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDatabaseMajorVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 30860c07-e84b-428a-922a-ba63c070cd9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 783247bda92e4a7dd3d89c6276be6457487f0bd0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67984194"
---
# <a name="getdatabasemajorversion-method-sqlserverdatabasemetadata"></a>Método getDatabaseMajorVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número da versão principal do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getDatabaseMajorVersion()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica a versão principal do banco de dados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getDatabaseMajorVersion é especificado pelo método getDatabaseMajorVersion na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
