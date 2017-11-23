---
title: "Método updateLong (int, long) | Microsoft Docs"
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
apiname: SQLServerResultSet.updateLong (int, long)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f6363288-1415-4b25-8bb3-c34d6211c6d7
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c0cb96da78af38a220862da9268b8b7c9f972b04
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="updatelong-method-int-long"></a>Método updateLong (int, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um **longo** valor, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateLong(int index,  
                       long x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *índice*  
  
 Um **int** que indica o índice da coluna.  
  
 *x*  
  
 Um **longo** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateLong é especificado pelo método updateLong na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateLong &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
