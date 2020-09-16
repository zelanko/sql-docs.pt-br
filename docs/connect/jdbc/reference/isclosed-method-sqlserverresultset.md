---
description: Método isClosed (SQLServerResultSet)
title: Método isClosed (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6081aa34-fc88-4dd0-9a3f-05e8488219dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c83e158dcb94f6fdf5b3ef2e9d1eedc5880e3d93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433578"
---
# <a name="isclosed-method-sqlserverresultset"></a>Método isClosed (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) foi fechado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se esse objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) estiver fechado, **false** se ele ainda estiver aberto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método isClosed é especificado pelo método isClosed na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
