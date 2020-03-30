---
title: Método getDisableStatementPooling (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 108bc70b3ff4a3fb03d332def79f9ceebeffd94a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67983631"
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>Método getDisableStatementPooling (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor da propriedade de conexão **disableStatementPooling**. Essa configuração controla se o pool de instruções está ou não habilitado para essa conexão.

  
## <a name="syntax"></a>Sintaxe  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **booliano** que contém o valor da propriedade de conexão **disableStatementPooling**.
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentários  
 Esse método está disponível no driver JDBC versão 6.4 e posteriores.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
