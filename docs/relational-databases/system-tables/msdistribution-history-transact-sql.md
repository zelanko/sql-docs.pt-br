---
title: MSdistribution_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 11e5be7e9f65c0df2cadc1d27ed0af85b214d7fc
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102754"
---
# <a name="msdistributionhistory-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdistribution_history** tabela contém linhas de histórico para os Distribution Agents associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do Distribution Agent.|  
|**runstatus**|**int**|O status de execução:<br /><br /> **1** = início.<br /><br /> **2** = êxito.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = repetição.<br /><br /> **6** = falha.|  
|**start_time**|**datetime**|A hora inicial de execução do trabalho.|  
|**time**|**datetime**|A hora de registro da mensagem.|  
|**duration**|**int**|A duração, em segundos, da sessão de mensagem.|  
|**Comentários**|**nvarchar(4000)**|O texto da mensagem.|  
|**xact_seqno**|**varbinary(16)**|O último número de sequência da transação processado.|  
|**current_delivery_rate**|**float**|O número médio de comandos fornecidos por segundo desde a última entrada de histórico.|  
|**current_delivery_latency**|**int**|A latência entre o comando que insere o banco de dados de distribuição e o aplicado ao Assinante desde a última entrada de histórico Em milissegundos.|  
|**delivered_transactions**|**int**|O número total de transações entregues na sessão.|  
|**delivered_commands**|**int**|O número total de comandos entregues na sessão.|  
|**average_commands**|**int**|O número médio de comandos entregues na sessão.|  
|**delivery_rate**|**float**|A média de comandos entregues por segundo.|  
|**delivery_latency**|**int**|A latência entre o comando que insere o banco de dados de distribuição e sendo aplicado ao Assinante. Em milissegundos.|  
|**total_delivered_commands**|**bigint**|O número total de comandos entregues desde que a assinatura foi criada.|  
|**error_id**|**int**|A ID do erro na **MSrepl_error** tabela do sistema.|  
|**updateable_row**|**bit**|Definido como **1** se a linha de histórico pode ser substituída.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
