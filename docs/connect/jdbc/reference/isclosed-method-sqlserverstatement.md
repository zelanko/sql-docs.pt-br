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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db0d1db2e274a7331d86cbaa58a309495c693520
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923556"
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
  
  
