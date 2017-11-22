---
title: "Método (SQLServerResultSet) deleteRow | Microsoft Docs"
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
apiname: SQLServerResultSet.deleteRow
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e6ee48f50f91e6c46099c5987df4c2f034398fe
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Exclui a linha atual deste[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto e do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void deleteRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método deleteRow é especificado pelo método deleteRow na interface Java.SQL. resultset.  
  
 Esse método não pode ser chamado quando o cursor estiver na linha de inserção.  
  
 Ao usar cursores do conjunto de chaves, esse método deixará um buraco no conjunto de resultados. Você pode testar esse buraco usando o [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) método. Os números de linha das linhas no conjunto de resultados não se alteram.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
