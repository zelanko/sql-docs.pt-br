---
title: Método getDriverVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDriverVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3be84d65-af61-4c34-b052-74a5d488eaa9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd67749bc8dcb29617c97a441c9858b3bb8fb6f5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983422"
---
# <a name="getdriverversion-method-sqlserverdatabasemetadata"></a>Método getDriverVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número de versão do driver JDBC em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getDriverVersion()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém a versão do driver JDBC.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getDriverVersion é especificado pelo método getDriverVersion na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
