---
title: "Método storesLowerCaseQuotedIdentifiers | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.storesLowerCaseQuotedIdentifiers
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 3e104c9e-66d4-436b-8b5b-a00ff667c95b
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b2bb8ea6754293a1b31d2bb4f769a283506a5f9
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="storeslowercasequotedidentifiers-method-sqlserverdatabasemetadata"></a>Método storesLowerCaseQuotedIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se este banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que estão entre aspas, sem diferenciar maiúsculas e minúsculas e os armazena em minúsculas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean storesLowerCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se os identificadores forem armazenados em minúsculas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método storesLowerCaseQuotedIdentifiers é especificado pelo método storesLowerCaseQuotedIdentifiers na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
