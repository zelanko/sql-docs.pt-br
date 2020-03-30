---
title: Método getMaxColumnNameLength (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 67fb5407-55b9-48b6-87f3-112700f304ba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab90493a897d5b9561f3e1f4f58413a5de8e8b9e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982314"
---
# <a name="getmaxcolumnnamelength-method-sqlserverdatabasemetadata"></a>Método getMaxColumnNameLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de caracteres que o banco de dados em questão permite para um nome de coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxColumnNameLength()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número máximo de caracteres permitidos.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getMaxColumnNameLength é especificado pelo método getMaxColumnNameLength na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
