---
description: Método nullsAreSortedAtEnd (SQLServerDatabaseMetaData)
title: Método nullsAreSortedAtEnd (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedAtEnd
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 713cf636-40f2-474a-8a5d-5aba4a310a9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b11b9868720a588ae60d63abad651af01193ca20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433158"
---
# <a name="nullsaresortedatend-method-sqlserverdatabasemetadata"></a>Método nullsAreSortedAtEnd (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se valores NULL são classificados no final, independentemente da ordem de classificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean nullsAreSortedAtEnd()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se estiver classificado no final. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método nullsAreSortedAtEnd é especificado pelo método nullsAreSortedAtEnd na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
