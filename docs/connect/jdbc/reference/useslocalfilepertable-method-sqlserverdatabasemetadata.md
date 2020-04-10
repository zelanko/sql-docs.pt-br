---
title: Método usesLocalFilePerTable (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.usesLocalFilePerTable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1fafb076-2bb7-4845-9c02-788479f00ca2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f0f2088f372b35059bbfaf480e90d94e6f277f9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919503"
---
# <a name="useslocalfilepertable-method-sqlserverdatabasemetadata"></a>Método usesLocalFilePerTable (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se este banco de dados usa um arquivo para cada tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean usesLocalFilePerTable()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** usa um arquivo para cada tabela. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método usesLocalFilePerTable é especificado pelo método usesLocalFilePerTable na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
