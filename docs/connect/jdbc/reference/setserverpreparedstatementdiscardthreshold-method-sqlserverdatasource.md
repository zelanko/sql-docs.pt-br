---
title: setServerPreparedStatementDiscardThreshold método (SQLServerDataSource) | Microsoft Docs
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
ms.topic: article
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4576e58df841cb0cfb4d33d68c5c90d355b5f379
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>setServerPreparedStatementDiscardThreshold método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor da propriedade de conexão serverPreparedStatementDiscardThreshold. Essa configuração controla quantos pendentes preparado descarte de instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Quando a configuração for < = 1 unprepare ações são executados imediatamente em Fechar instrução preparada. Se o valor é definido como 1 > estas chamadas são em lote juntos para evitar a sobrecarga da chamada sp_unprepare com muita frequência
 
## <a name="syntax"></a>Sintaxe  
  
```
public void setServerPreparedStatementDiscardThreshold(int enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *serverPreparedStatementDiscardThreshold*  
  
 O novo valor da **serverPreparedStatementDiscardThreshold** propriedade de conexão.  

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
