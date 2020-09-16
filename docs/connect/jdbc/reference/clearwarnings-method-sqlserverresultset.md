---
description: Método clearWarnings (SQLServerResultSet)
title: Método clearWarnings (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.clearWarnings
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f55af4b6-ae5c-41c9-8aa3-8313773f5443
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac3142b51903d43c3dc9f9ba9ee63becfc810c00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438128"
---
# <a name="clearwarnings-method-sqlserverresultset"></a>Método clearWarnings (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Limpa todos os avisos relatados sobre este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
> [!NOTE]  
>  No momento, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não implementa esse método. Se chamado, ele retornará nulo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void clearWarnings()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método clearWarnings é especificado pelo método clearWarnings na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
