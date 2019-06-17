---
title: Feche o Driver JDBC conjuntos de resultados abertos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1739ecb5-e5cb-4807-b5a8-97c0299929d0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fc9a0629c15f98008cfd35f5ff6ab4203b12f05f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803681"
---
# <a name="autocommitfailureclosesallresultsets-method-sqlserverdatabasemetadata"></a>Método autoCommitFailureClosesAllResultSets (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o driver JDBC fecha todos os conjuntos de resultados abertos, inclusive aqueles colocados em espera, quando uma confirmação automática é habilitada e uma exceção é lançada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean autoCommitFailureClosesAllResultSets()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se resultar a abrir todos os conjuntos, inclusive aqueles, são fechados quando uma confirmação automática é habilitada e uma exceção será gerada. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método autoCommitFailureClosesAllResultSets é especificado pelo método autoCommitFailureClosesAllResultSets na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
