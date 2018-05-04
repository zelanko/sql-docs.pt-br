---
title: MSlogreader_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSlogreader_history_TSQL
- MSlogreader_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_history system table
ms.assetid: 2e399fa1-3591-4c1c-96b7-7964fe82c7c4
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2971d515327089de4c528bdc9ee661b7598de5c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mslogreaderhistory-transact-sql"></a>MSlogreader_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSlogreader_history** tabela contém linhas de histórico para o Log Reader Agents associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**Int**|A ID do Log Reader Agent.|  
|**runstatus**|**Int**|O status da execução:<br /><br /> 1 = Iniciar.<br /><br /> 2 = Êxito.<br /><br /> 3 = Em andamento.<br /><br /> 4 = Inativo.<br /><br /> 5 = Repetir.<br /><br /> 6 = Falha.|  
|**start_time**|**datetime**|A hora inicial de execução do trabalho.|  
|**time**|**datetime**|A hora de registro da mensagem.|  
|**duration**|**Int**|A duração, em segundos, da sessão de mensagem.|  
|**Comentários**|**nvarchar(255)**|O texto da mensagem.|  
|**xact_seqno**|**varbinary(16)**|O último número de sequência da transação processado.|  
|**delivery_time**|**Int**|A hora de entrega da primeira transação.|  
|**delivered_transactions**|**Int**|O número total de transações entregues na sessão.|  
|**delivered_commands**|**Int**|O número total de comandos entregues na sessão.|  
|**average_commands**|**Int**|O número médio de comandos entregues na sessão.|  
|**delivery_rate**|**float**|A média de comandos entregues por segundo.|  
|**delivery_latency**|**Int**|A latência entre o comando que insere o banco de dados publicado e sendo inserido no banco de dados de distribuição. Em milissegundos.|  
|**error_id**|**Int**|A ID do erro no **MSrepl_error** tabela do sistema.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
|**updateable_row**|**bit**|Definido como **1** se a linha de histórico pode ser substituída.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
