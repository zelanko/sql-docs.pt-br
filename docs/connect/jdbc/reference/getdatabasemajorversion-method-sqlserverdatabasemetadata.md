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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 486b064aaac56599379aa1a52fa24ff075d771ae
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923237"
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
  
  
