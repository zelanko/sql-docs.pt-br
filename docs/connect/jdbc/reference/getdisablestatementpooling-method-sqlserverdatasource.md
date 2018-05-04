---
title: getDisableStatementPooling método (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6038ae342949313fd65c70fd2f9bb84b5df5e08
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>getDisableStatementPooling método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor de **disableStatementPooling** propriedade de conexão. Essa configuração controla se o pooling de instrução está habilitada ou não para essa conexão.

  
## <a name="syntax"></a>Sintaxe  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **booliano** que contém o valor de **disableStatementPooling** propriedade de conexão.
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
