---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2f5178c8a2ce5b527ce70e6a3d8fc139ccc9c72
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977204"
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
  
  
