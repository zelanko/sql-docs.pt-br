---
title: Método (SQLServerConnection) setHoldability | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 60d46f8f8792eacd7f1f67a67b2fc9fc56bf5a8e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764465"
---
# <a name="setholdability-method-sqlserverconnection"></a>Método setHoldability (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Altera a funcionalidade de suspensão de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) criados com o uso do objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) em questão para a capacidade de colocação em espera fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nNewHold*  
  
 Um valor **int** que contém um dos seguintes níveis de suspensão:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setHoldability é especificado pelo método setHoldability na interface do Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
