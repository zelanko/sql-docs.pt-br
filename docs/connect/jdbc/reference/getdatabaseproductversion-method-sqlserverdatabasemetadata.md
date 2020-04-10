---
title: Método getDatabaseProductVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDatabaseProductVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19c0c15d-223f-45bd-a215-2867dfefecb0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd09db3880b7e4294620f9e8f0476fc759d1a54a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923192"
---
# <a name="getdatabaseproductversion-method-sqlserverdatabasemetadata"></a>Método getDatabaseProductVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número da versão do produto de banco de dados em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getDatabaseProductVersion()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o número de versão de produto no banco de dados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getDatabaseProductVersion é especificado pelo método getDatabaseProductVersion na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
