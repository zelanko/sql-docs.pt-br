---
title: "Método (SQLServerStatement) setMaxFieldSize | Microsoft Docs"
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
apiname: SQLServerStatement.setMaxFieldSize
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 38f7fc1d-acad-4d10-9fc8-3c0669d93b07
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d46ffc9f85b156fb4c36b56eeddc0d53d78b36c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setmaxfieldsize-method-sqlserverstatement"></a>setMaxFieldSize método (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o limite para o número máximo de bytes em uma [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) coluna armazena caracteres ou valores binários, como o número de bytes fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setMaxFieldSize(int max)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Max*  
  
 Um **int** que indica o número máximo de bytes.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setMaxFieldSize é especificado pelo método setMaxFieldSize na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
