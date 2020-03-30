---
title: Método supportsCatalogsInTableDefinitions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInTableDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e1e50ac-f3d4-416a-8a69-d8b7b4f30bf3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa1c949cab59b1ff04f9cb0ae693b037fd3588f9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67969661"
---
# <a name="supportscatalogsintabledefinitions-method-sqlserverdatabasemetadata"></a>Método supportsCatalogsInTableDefinitions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se um nome de catálogo pode ser usado em uma instrução de definição de tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsCatalogsInTableDefinitions()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método supportsCatalogsInTableDefinitions é especificado pelo método supportsCatalogsInTableDefinitions na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
