---
title: "Método storesUpperCaseQuotedIdentifiers | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.storesUpperCaseQuotedIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 936ec140-2597-44e6-82d3-3994a676ee35
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36649209e8e9b6c3073f7463ae2bd46d086c4222
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="storesuppercasequotedidentifiers-method-sqlserverdatabasemetadata"></a>Método storesUpperCaseQuotedIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que estão entre aspas, como sem diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean storesUpperCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se os identificadores forem armazenados em maiusculas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método storesUpperCaseQuotedIdentifiers é especificado pelo método storesUpperCaseQuotedIdentifiers na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

