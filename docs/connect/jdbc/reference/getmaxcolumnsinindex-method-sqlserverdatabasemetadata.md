---
title: Método getMaxColumnsInIndex (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getMaxColumnsInIndex
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 108f0e2c-7dc5-4195-8248-0758a75a314e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6409b558aaf533bad585655426ad0bb3ca690f42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getmaxcolumnsinindex-method-sqlserverdatabasemetadata"></a>Método getMaxColumnsInIndex (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de colunas que o banco de dados em questão permite em um índice.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxColumnsInIndex()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número máximo de colunas permitidas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMaxColumnsInIndex é especificado pelo método getMaxColumnsInIndex na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
