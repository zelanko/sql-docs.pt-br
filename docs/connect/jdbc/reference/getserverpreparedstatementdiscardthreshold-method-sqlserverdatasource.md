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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef993e25397be7e8aca1a4b83357bf95ae88693c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925350"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>Método getServerPreparedStatementDiscardThreshold (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor da propriedade de conexão **serverPreparedStatementDiscardThreshold**. Essa configuração controla quantas ações de descarte de instruções preparadas pendentes (sp_unprepare) podem estar pendentes por conexão antes que uma chamada para limpar os identificadores pendentes no servidor seja executada. Quando a configuração é < = 1, ações de cancelamento de preparação são executadas imediatamente no fechamento da instrução preparada. Se esse valor for definido como > 1, essas chamadas serão agrupadas em lote para evitar a sobrecarga de chamar sp_unprepare com muita frequência.

  
## <a name="syntax"></a>Sintaxe  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna o valor **int** da propriedade de conexão **serverPreparedStatementDiscardThreshold**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentários  
 Esse método está disponível no driver JDBC versão 6.4 e posteriores.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
