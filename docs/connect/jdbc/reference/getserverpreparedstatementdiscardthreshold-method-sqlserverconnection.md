---
title: getServerPreparedStatementDiscardThreshold método (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ff0c7fcda4a814d3e9e1347c2b04fb89f699e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32837362"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold método (SQLServerConnection)
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
  
  
