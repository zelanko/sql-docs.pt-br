---
title: "Método getMaxUserNameLength (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.getMaxUserNameLength
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 09ec7d40-4c4a-4d89-ba11-78e5327b5759
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 114d734348b41ffee81341ec1dafec0304067678
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="getmaxusernamelength-method-sqlserverdatabasemetadata"></a>Método getMaxUserNameLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de caracteres que o banco de dados em questão permite em um nome de usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxUserNameLength()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número máximo de caracteres permitidos.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getMaxUserNameLength é especificado pelo método getMaxUserNameLength na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
