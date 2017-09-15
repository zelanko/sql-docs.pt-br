---
title: Feche o Driver JDBC conjuntos de resultados abertos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1739ecb5-e5cb-4807-b5a8-97c0299929d0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f2f09f2eacf96ccebb88376ba3866d4188b377d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# Método autoCommitFailureClosesAllResultSets (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o driver JDBC fecha todos os conjuntos de resultados abertos, inclusive aqueles colocados em espera, quando uma confirmação automática é habilitada e uma exceção é lançada.  
  
## Sintaxe  
  
```  
  
public boolean autoCommitFailureClosesAllResultSets()  
```  
  
## Valor de retorno  
 **True** se resultar abrir todos os conjuntos, inclusive aqueles, forem fechados quando uma confirmação automática está habilitada e uma exceção é gerada. Caso contrário, **false**.  
  
## Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Comentários  
 Esse método autoCommitFailureClosesAllResultSets é especificado pelo método autoCommitFailureClosesAllResultSets na interface DatabaseMetadata.  
  
## Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

