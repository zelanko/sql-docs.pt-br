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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983631"
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>Método getDisableStatementPooling (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor da propriedade de conexão **disableStatementPooling** . Essa configuração controla se o pooling de instruções está habilitado ou não para essa conexão.

  
## <a name="syntax"></a>Sintaxe  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **booliano** que contém o valor da propriedade de conexão **disableStatementPooling** .
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método está disponível no JDBC Driver versão 6,4 e em diante.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
