---
title: Método (Java, short) updateShort | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateShort (java.lang.String, short)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e596e99-11ce-4a57-b247-e40078922036
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20fdf43795327c42c68b815dcb2e151e0bbe131e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updateshort-method-javalangstring-short"></a>Método updateShort (java.lang.String, short)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um **curto** valor, considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateShort(java.lang.String columnName,  
                        short x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
 *x*  
  
 Um **curto** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateShort é especificado pelo método updateShort na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateShort &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
