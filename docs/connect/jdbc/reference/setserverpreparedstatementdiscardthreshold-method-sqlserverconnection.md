---
title: Método setServerPreparedStatementDiscardThreshold (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f66746b15e96f49d96b428e8cf8844eeea12a12
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972923"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>Método setServerPreparedStatementDiscardThreshold (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Especifica o comportamento de uma instância de conexão específica. Essa configuração controla quantas ações de descarte de instruções preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Quando a configuração é < = 1, ações de cancelamento de preparação são executadas imediatamente no fechamento da instrução preparada. Se o valor for definido como > 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência.


## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>parâmetros  
 *thresholdValue*  
 
 O novo valor da propriedade de conexão **serverPreparedStatementDiscardThreshold**.  
 
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentários  
 Esse método está disponível no JDBC Driver versão 6.4 e em diante.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
