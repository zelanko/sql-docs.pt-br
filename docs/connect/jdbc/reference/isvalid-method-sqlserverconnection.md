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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 379d71b2100115bc1192a6f8f744b5afe92e5aed
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921082"
---
# <a name="isvalid-method-sqlserverconnection"></a>Método isValid (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) não foi fechado e ainda é válido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *timeout*  
  
 Um **int** que especifica o número de segundos de espera para validação a conexão.  
  
## <a name="return-value"></a>Valor retornado  
 **true** se a conexão for válida; **false** se a conexão não for válida ou se a validade da conexão não puder ser determinada antes da expiração do tempo limite.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método isValid é especificado pelo método isValid na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
