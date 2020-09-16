---
description: Método cancelRowUpdates (SQLServerResultSet)
title: Método cancelRowUpdates (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.cancelRowUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ecacca4-f7bc-4f5d-886a-da7747fdccae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32e5333f571ff9375bdbdc61e9743d29a57cedfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438178"
---
# <a name="cancelrowupdates-method-sqlserverresultset"></a>Método cancelRowUpdates (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cancela as atualizações feitas na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void cancelRowUpdates()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método cancelRowUpdates é especificado pelo método cancelRowUpdates na interface java.sql.ResultSet.  
  
 Esse método pode ser chamado depois da chamada de um método updater e antes da chamada do método [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para reverter as atualizações que foram feitas em uma linha. Se nenhuma atualização for feita ou se updateRow já tiver sido chamado, esse método não terá nenhum efeito.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
