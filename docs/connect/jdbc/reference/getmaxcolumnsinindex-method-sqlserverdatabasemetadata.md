---
title: Método getMaxColumnsInIndex (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInIndex
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 108f0e2c-7dc5-4195-8248-0758a75a314e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f98d3bdb5e893d1c120be059e1ad1de446dc8d6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982254"
---
# <a name="getmaxcolumnsinindex-method-sqlserverdatabasemetadata"></a>Método getMaxColumnsInIndex (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de colunas que o banco de dados em questão permite em um índice.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxColumnsInIndex()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número máximo de colunas permitidas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getMaxColumnsInIndex é especificado pelo método getMaxColumnsInIndex na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
