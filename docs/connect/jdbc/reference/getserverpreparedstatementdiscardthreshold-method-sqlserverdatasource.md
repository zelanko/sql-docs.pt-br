---
title: Método getServerPreparedStatementDiscardThreshold (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 3f91b75b5c70029d53582b8b6ed4655485fd3fcf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979898"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>Método getServerPreparedStatementDiscardThreshold (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor da propriedade de conexão **serverPreparedStatementDiscardThreshold** . Essa configuração controla quantas ações de descarte de instrução preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Quando a configuração é < = 1 as ações despreparar são executadas imediatamente no fechamento da instrução preparada. Se esse valor estiver definido como > 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência.

  
## <a name="syntax"></a>Sintaxe  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna o valor **int** da propriedade de conexão **serverPreparedStatementDiscardThreshold** .  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método está disponível no JDBC Driver versão 6,4 e em diante.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
