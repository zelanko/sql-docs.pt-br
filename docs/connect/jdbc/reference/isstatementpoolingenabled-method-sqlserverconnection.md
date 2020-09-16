---
description: Método isStatementPoolingEnabled (SQLServerConnection)
title: Método isStatementPoolingEnabled (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isStatementPoolingEnabled
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 76c6afdec909de1edce177e05599b37b4fa8c746
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433358"
---
# <a name="isstatementpoolingenabled-method-sqlserverconnection"></a>Método isStatementPoolingEnabled (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Retorna a condição do pool de instruções (habilitado ou não) para essa conexão.

## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isStatementPoolingEnabled()  
```  

## <a name="return-value"></a>Valor retornado
 Um **booliano** que contém o sinalizador que indica se o pool de instruções está habilitado ou não.

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentários  
 Esse método está disponível no driver JDBC versão 6.4 e posteriores.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
