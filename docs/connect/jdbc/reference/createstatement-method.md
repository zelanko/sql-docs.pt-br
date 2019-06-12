---
title: Método createStatement () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 480f21b6-50cc-4b1e-a0b0-8774ecfe94f1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 340c37a2e5e162af3ab2ae80813b14c6bab7a0f9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772893"
---
# <a name="createstatement-method-"></a>Método createStatement ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) para enviar instruções SQL ao banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Statement createStatement()  
```  
  
## <a name="return-value"></a>Valor retornado  
 O objeto de instrução.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método prepareStatement é especificado pelo método prepareStatement na interface do Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
