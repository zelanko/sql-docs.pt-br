---
title: Método isValid (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6313844442f651fb64127ef0b591f1c0ffda363
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="isvalid-method-sqlserverconnection"></a>Método isValid (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto não foi fechado e ainda é válido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *timeout*  
  
 Um **int** que especifica o número de segundos de espera para validar a conexão.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a conexão for válida; **false** se a conexão não é válido ou não é possível determinar a validade da conexão antes do tempo limite expirar.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isValid é especificado pelo método isValid na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
