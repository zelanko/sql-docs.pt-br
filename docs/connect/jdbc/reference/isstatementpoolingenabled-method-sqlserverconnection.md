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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dff9c558351dc4228eab21ac759dae6c58b4cb97
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925320"
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
  
  
