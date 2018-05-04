---
title: Método supportsMixedCaseIdentifiers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMixedCaseIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0f68d9f7-0d8d-4d8d-9188-14e253a2576a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73a1077b67ec6aa87b189fc6b2c768ebbacfd6ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supportsmixedcaseidentifiers-method-sqlserverdatabasemetadata"></a>Método supportsMixedCaseIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se o banco de dados em questão trata os identificadores SQL que usam maiúsculas e minúsculas, e que não estão entre aspas, com diferenciação de maiúsculas e minúsculas e os armazena em maiúsculas e minúsculas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsMixedCaseIdentifiers()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se os identificadores forem armazenados em maiusculas e minúsculas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsMixedCaseIdentifiers é especificado pelo método supportsMixedCaseIdentifiers na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
