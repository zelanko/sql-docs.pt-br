---
title: "Método getMaxIndexLength (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getMaxIndexLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c85d021-d466-4732-85f9-53903d297041
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7dd9922da6bd519d9f2c02599ec88a2d481a7bc9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getmaxindexlength-method-sqlserverdatabasemetadata"></a>Método getMaxIndexLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de bytes que o banco de dados permite para um índice, incluindo todas as suas partes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxIndexLength()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número máximo de bytes permitidos.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getMaxIndexLength é especificado pelo método getMaxIndexLength na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

