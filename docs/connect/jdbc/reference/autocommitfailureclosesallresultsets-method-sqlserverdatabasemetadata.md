---
description: Método autoCommitFailureClosesAllResultSets (SQLServerDatabaseMetaData)
title: O JDBC Driver fecha conjuntos de resultados abertos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1739ecb5-e5cb-4807-b5a8-97c0299929d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e0fb75b6124947cd32656d081d0c3a29c327b63b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438208"
---
# <a name="autocommitfailureclosesallresultsets-method-sqlserverdatabasemetadata"></a>Método autoCommitFailureClosesAllResultSets (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o driver JDBC fecha todos os conjuntos de resultados abertos, inclusive aqueles colocados em espera, quando uma confirmação automática é habilitada e uma exceção é lançada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean autoCommitFailureClosesAllResultSets()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se todos os conjuntos de resultados abertos, inclusive aqueles colocados em espera, forem fechados quando uma confirmação automática é habilitada e uma exceção é gerada. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método autoCommitFailureClosesAllResultSets é especificado pelo método autoCommitFailureClosesAllResultSets na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
