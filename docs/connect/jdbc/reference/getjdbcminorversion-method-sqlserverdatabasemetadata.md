---
title: Método getJDBCMinorVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getJDBCMinorVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d9e153b5-51b7-4e44-b342-f147f04dbe19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 600c1369df2bf71f305ccd10937f9b901212ac98
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921414"
---
# <a name="getjdbcminorversion-method-sqlserverdatabasemetadata"></a>Método getJDBCMinorVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número da versão secundária do JDBC para esse driver.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getJDBCMinorVersion()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica a versão secundária do JDBC.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getJDBCMinorVersion é especificado pelo método getJDBCMinorVersion na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
