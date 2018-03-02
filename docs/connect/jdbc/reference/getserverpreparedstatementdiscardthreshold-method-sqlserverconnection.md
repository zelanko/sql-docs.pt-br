---
title: "getServerPreparedStatementDiscardThreshold método (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 680c7fe2fe0802054f56008701af48baea4ac98b
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold Method (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Retorna o valor de **serverPreparedStatementDiscardThreshold** propriedade de conexão. Essa configuração controla quantos pendentes preparado descarte de instrução ações (sp_unprepare) podem estar pendentes por conexão antes de uma chamada para limpar os identificadores pendentes no servidor é executada. Se a configuração for < = 1, unprepare ações são executadas imediatamente em Fechar instrução preparada. Se estiver definido como 1 >, estas chamadas são agrupadas para evitar a sobrecarga da chamada sp_unprepare com muita frequência. O padrão para essa opção pode ser alterado pela chamada getDefaultServerPreparedStatementDiscardThreshold().

## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>Valor de retorno
 Um **int** que contém o valor de **serverPreparedStatementDiscardThreshold** propriedade de conexão.

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
