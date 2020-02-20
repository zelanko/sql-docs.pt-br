---
title: Método getDisableStatementPooling (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getDisableStatementPooling
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2da0a2f04fa90b2d25dbd68baf7b769d5afdcf8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983644"
---
# <a name="getdisablestatementpooling-method-sqlserverconnection"></a>Método getDisableStatementPooling (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Retorna o valor da propriedade de conexão **disableStatementPooling**. Essa configuração controla se o pool de instruções está ou não habilitado para essa conexão.

## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getDisableStatementPooling()  
```  

## <a name="return-value"></a>Valor retornado
 Um **booliano** que contém o valor da propriedade de conexão **disableStatementPooling**.

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentários  
 Esse método está disponível no JDBC Driver versão 6.4 e em diante.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
