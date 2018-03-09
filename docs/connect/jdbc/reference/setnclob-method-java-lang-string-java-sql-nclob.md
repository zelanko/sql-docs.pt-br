---
title: "Método setNClob (Java, Java.SQL. NCLOB) | Microsoft Docs"
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
ms.assetid: 4e30d242-0c1b-45db-b75f-41b041692f31
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e920c0079bd431926a669ff2fd0033d2bc051dd
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setnclob-method-javalangstring-javasqlnclob"></a>Método setNClob (java.lang.String, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto NClob especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nome do parâmetro*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
 *value*  
  
 Um objeto NClob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método deve ser usado para **NCHAR**, **NVARCHAR**, **NTEXT**, e **XML** tipos de dados do parâmetro.  
  
 Esse método setNClob é especificado pelo método setNClob na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método setNClob &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
