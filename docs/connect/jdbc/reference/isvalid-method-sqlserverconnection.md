---
title: "Método isValid (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed5a2cb3da3fd5ac503f002f3da3dd4dd90a3e77
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="isvalid-method-sqlserverconnection"></a>Método isValid (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto não foi fechado e ainda é válido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *tempo limite*  
  
 Um **int** que especifica o número de segundos de espera para validar a conexão.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a conexão for válida; **false** se a conexão não é válido ou não é possível determinar a validade da conexão antes do tempo limite expirar.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método isValid é especificado pelo método isValid na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

