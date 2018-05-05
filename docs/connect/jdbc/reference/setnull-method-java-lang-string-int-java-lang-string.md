---
title: Método setNull (Java, int, Java) | Microsoft Docs
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
- SQLServerCallableStatement.setNull (java.lang.String, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16ff77f9-7928-415c-abf6-97ed59e3e396
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e819135ec2f8aa6c93e2d34291b1855a9fdb3904
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setnull-method-javalangstring-int-javalangstring"></a>Método setNull (java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como um valor nulo, considerando o tipo e o nome do parâmetro a ser definido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType,  
                    java.lang.String sTypeName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Um **cadeia de caracteres** contthat contém aining o nome do parâmetro.  
  
 *nType*  
  
 Um código do tipo de JDBC que é definido pelo java.sql.Types.  
  
 *sTypeName*  
  
 Um **cadeia de caracteres** que indica o nome totalmente qualificado do parâmetro que está sendo definido.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setNull é especificado pelo método na interface do CallableStatement setNull.  
  
## <a name="see-also"></a>Consulte também  
 [Método setNull &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
