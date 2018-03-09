---
title: "Método (SQLServerResultSet) rowUpdated | Microsoft Docs"
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
apiname: SQLServerResultSet.rowUpdated
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0adc297c74a700312d3d0ffdc9640dd7b25595e8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="rowupdated-method-sqlserverresultset"></a>rowUpdated método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se a linha atual foi atualizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a linha foi atualizada visivelmente pelo proprietário ou outro usuário, e as atualizações são detectadas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método rowUpdated é especificado pelo método rowUpdated na interface Java.SQL. resultset.  
  
 O valor que é retornado dependerá da capacidade do conjunto de resultados de detectar atualizações.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]não detecta linhas atualizadas para qualquer tipo de cursor.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
