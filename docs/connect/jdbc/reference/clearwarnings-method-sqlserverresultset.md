---
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
ms.openlocfilehash: d77d6130fd50fd6376c81eeb1af497b8bf25e3af
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923673"
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
  
  
