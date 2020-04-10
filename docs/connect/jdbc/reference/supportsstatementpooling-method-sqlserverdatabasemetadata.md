---
title: Método supportsStatementPooling (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsStatementPooling
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 83777807-5838-4f81-94ab-3ba4fc5aaa47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3431fe93b64c441f10537a6b0def63ae4748cf3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928461"
---
# <a name="supportsstatementpooling-method-sqlserverdatabasemetadata"></a>Método supportsStatementPooling (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte ao pooling de instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsStatementPooling()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método supportsStatementPooling é especificado pelo método supportsStatementPooling na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
