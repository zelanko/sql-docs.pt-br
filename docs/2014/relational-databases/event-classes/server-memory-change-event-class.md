---
title: Classe de evento Server Memory Change | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Server Memory Change event class
ms.assetid: c9836484-39c5-4a89-b080-3567783b6fff
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4dfa610b7632455c5d7d7a84efcb6101ffc7575b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052515"
---
# <a name="server-memory-change-event-class"></a>classe de evento Server Memory Change
  A classe de evento **Server Memory Change** ocorre quando o uso de memória do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aumenta ou diminui em 1 MB (megabyte) ou em 5% da memória máxima do servidor, o que for maior.  
  
## <a name="server-memory-change-event-class-data-columns"></a>Colunas de dados da classe de evento Server Memory Change  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Sim|  
|----------------------|---------------|-----------------|---------------|---------|  
|**EventClass**|**int**|Tipo de evento = 81.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**EventSubClass**|**int**|Tipo de subclasse de evento.<br /><br /> 1 = Aumento de memória<br /><br /> 2 = Diminuição de memória|21|Sim|  
|**IntegerData**|**int**|Novo tamanho da memória, em megabytes (MB).|25|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|O nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|**XactSequence**|**bigint**|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
