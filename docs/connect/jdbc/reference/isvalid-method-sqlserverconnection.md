---
title: Método isValid (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2868fb92161b5e3458e5c5e0dc72ebdef074b3e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796317"
---
# <a name="isvalid-method-sqlserverconnection"></a>Método isValid (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) não foi fechado e ainda é válido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *timeout*  
  
 Um **int** que especifica o número de segundos de espera para validação a conexão.  
  
## <a name="return-value"></a>Valor retornado  
 **True** se a conexão for válida. **falsos** se a conexão não é válido ou não é possível determinar a validade da conexão antes do tempo limite expirar.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isValid é especificado pelo método isValid na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
