---
title: "Método (Java) getNClob | Microsoft Docs"
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
ms.assetid: be01ce56-8f13-437b-8de6-246cda5f7830
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd11b3bc0f6a43ffcc504b99b117e3eab5170749
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getnclob-method-javalangstring"></a>Método getNClob (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor de um JDBC **NCLOB** parâmetro como um objeto NClob na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.NClob getNClob(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nome do parâmetro*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 ANClobobject.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getNClob é especificado pelo método getNClob na interface do CallableStatement.  
  
 Este método oferece suporte somente à recuperação **NCHAR**, **NVARCHAR**, **NTEXT**, e **XML** parâmetros. Chamar esses métodos em outros parâmetros de tipo de dados causará uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Método getNClob &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

