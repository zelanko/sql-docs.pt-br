---
description: Método supportsCatalogsInIndexDefinitions (SQLServerDatabaseMetaData)
title: Método supportsCatalogsInIndexDefinitions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInIndexDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a19423a0-e7b6-4f5c-94be-80ddf3fa4717
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e385c2782ed45ecb2353b01f583e9b3aedc55b7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462476"
---
# <a name="supportscatalogsinindexdefinitions-method-sqlserverdatabasemetadata"></a>Método supportsCatalogsInIndexDefinitions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se um nome de catálogo pode ser usado em uma instrução de definição de índice.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsCatalogsInIndexDefinitions()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método supportsCatalogsInIndexDefinitions é especificado pelo método supportsCatalogsInIndexDefinitions na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
