---
title: "Método (Java) getURL | Microsoft Docs"
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
apiname: SQLServerCallableStatement.getURL (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: eb709f6b-64e1-4d0c-a704-290891627dd7
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d644f0fab52324edaabcba1c8d2bde2a36d42b85
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="geturl-method-javalangstring"></a>Método getURL (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto na linguagem de programação Java considerando o nome do parâmetro de URL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.net.URL getURL(java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *s*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de URL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getURL é especificado pelo método getURL na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método getURL &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
