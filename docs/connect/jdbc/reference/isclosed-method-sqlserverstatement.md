---
title: Método isClosed (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e79b5b53-16b0-42a3-be4e-542a77a21e12
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe4d41448fdd65d3cb4a56f873432e747f564ef6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977706"
---
# <a name="isclosed-method-sqlserverstatement"></a>Método isClosed (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) foi fechado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se esse objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) estiver fechado, **false** se ele ainda estiver aberto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método isClosed é especificado pelo método isClosed na interface java.sql.Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
