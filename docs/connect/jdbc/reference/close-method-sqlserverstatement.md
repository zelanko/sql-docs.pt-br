---
description: Método close (SQLServerStatement)
title: Método close (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 84a25d64-dd3e-4696-bb5f-4eaf391fab7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5162697f7f19c8de6c8546c65c853e241f8f131d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438068"
---
# <a name="close-method-sqlserverstatement"></a>Método close (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Libera imediatamente o banco de dados e os recursos do JDBC do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), em vez de aguardar que eles sejam liberados automaticamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método close é especificado pelo método close na interface java.sql.Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
