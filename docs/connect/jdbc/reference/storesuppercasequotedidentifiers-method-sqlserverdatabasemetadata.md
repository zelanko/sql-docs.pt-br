---
title: Método storesUpperCaseQuotedIdentifiers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.storesUpperCaseQuotedIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 936ec140-2597-44e6-82d3-3994a676ee35
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5388b0f162373ba6fb933ff20182ae819963bdba
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969873"
---
# <a name="storesuppercasequotedidentifiers-method-sqlserverdatabasemetadata"></a>Método storesUpperCaseQuotedIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados trata identificadores de SQL que usam maiúsculas e minúsculas, e que estão entre aspas, como sem diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean storesUpperCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se os identificadores forem armazenados em maiúsculas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método storesUpperCaseQuotedIdentifiers é especificado pelo método storesUpperCaseQuotedIdentifiers na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
