---
title: getServerPreparedStatementDiscardThreshold método (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 9281981535d24187e8408313e13264627720cd45
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor de **serverPreparedStatementDiscardThreshold** propriedade de conexão. Essa configuração controla quantos pendentes preparado descarte de instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Quando a configuração for < = 1 unprepare ações são executados imediatamente em Fechar instrução preparada. Se esse valor é definido como 1 > estas chamadas são agrupadas para evitar a sobrecarga da chamada sp_unprepare com muita frequência.

  
## <a name="syntax"></a>Sintaxe  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna o **int** valor o **serverPreparedStatementDiscardThreshold** propriedade de conexão.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
