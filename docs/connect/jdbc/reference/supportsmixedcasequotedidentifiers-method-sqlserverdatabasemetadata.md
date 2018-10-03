---
title: Método supportsMixedCaseQuotedIdentifiers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMixedCaseQuotedIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 76c68fc2-5af6-4b8d-baee-245716fdc5cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a01c246d7388c8a10641997af28bb97778cbb4f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666014"
---
# <a name="supportsmixedcasequotedidentifiers-method-sqlserverdatabasemetadata"></a>Método supportsMixedCaseQuotedIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados trata os identificadores SQL que usam maiúsculas e minúsculas, e que estão entre aspas, como fazendo diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas e minúsculas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsMixedCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se os identificadores são armazenados em maiusculas e minúsculas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsMixedCaseQuotedIdentifiers é especificado pelo método supportsMixedCaseQuotedIdentifiers na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
