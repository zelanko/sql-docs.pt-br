---
title: Método supportsExtendedSQLGrammar (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsExtendedSQLGrammar
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8deb1987-c4e3-4599-8e37-0a04ec20b480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d049336def80d1856f04ff22b1375b540f940858
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924385"
---
# <a name="supportsextendedsqlgrammar-method-sqlserverdatabasemetadata"></a>Método supportsExtendedSQLGrammar (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte à gramática de SQL estendida do ODBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsExtendedSQLGrammar()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método supportsExtendedSQLGrammer é especificado pelo método supportsExtendedSQLGrammer method na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
