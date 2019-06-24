---
title: Método getMaxColumnsInGroupBy (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInGroupBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a59cfe98-c0f4-46ad-9243-62aa56855f1a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d1d4c45f9d7f1ac3b8e5397b48563723fe910dee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66792757"
---
# <a name="getmaxcolumnsingroupby-method-sqlserverdatabasemetadata"></a>Método getMaxColumnsInGroupBy (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de colunas que o banco de dados permite em uma cláusula GROUP BY.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxColumnsInGroupBy()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número máximo de colunas permitidas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMaxColumnsInGroupBy é especificado pelo método getMaxColumnsInGroupBy na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
