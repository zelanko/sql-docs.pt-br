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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af86780bc2c54dfa504c63d2fc18f11e8bf22f2c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80917563"
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
 Esse método está disponível no driver JDBC versão 6.4 e posteriores.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
