---
title: Método getMaxProcedureNameLength (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxProcedureNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1c05eb3-8465-46fd-99bc-5e8effcafee5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90bb02725131a3e770c6471a956ee02f73a293c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getmaxprocedurenamelength-method-sqlserverdatabasemetadata"></a>Método getMaxProcedureNameLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de caracteres que esse banco de dados permite em um nome de procedimento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxProcedureNameLength()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número máximo de caracteres permitidos.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMaxProcedureNameLength é especificado pelo método getMaxProcedureNameLength na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
