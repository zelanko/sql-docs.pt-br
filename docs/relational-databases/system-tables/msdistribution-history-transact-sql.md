---
title: MSdistribution_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1053181486dba8c8119f9160d9c08cb8d2bbe56b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907388"
---
# <a name="msdistribution_history-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSdistribution_history** contém linhas de histórico para os agentes de distribuição associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do Distribution Agent.|  
|**runstatus**|**int**|O status de execução:<br /><br /> **1** = iniciar.<br /><br /> **2** = com sucesso.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = tentar novamente.<br /><br /> **6** = falha.|  
|**start_time**|**datetime**|A hora inicial de execução do trabalho.|  
|**time**|**datetime**|A hora de registro da mensagem.|  
|**permanência**|**int**|A duração, em segundos, da sessão de mensagem.|  
|**feitos**|**nvarchar(4000)**|O texto da mensagem.|  
|**xact_seqno**|**varbinary (16)**|O último número de sequência da transação processado.|  
|**current_delivery_rate**|**float**|O número médio de comandos fornecidos por segundo desde a última entrada de histórico.|  
|**current_delivery_latency**|**int**|A latência entre o comando que insere o banco de dados de distribuição e o aplicado ao Assinante desde a última entrada de histórico Em milissegundos.|  
|**delivered_transactions**|**int**|O número total de transações entregues na sessão.|  
|**delivered_commands**|**int**|O número total de comandos entregues na sessão.|  
|**average_commands**|**int**|O número médio de comandos entregues na sessão.|  
|**delivery_rate**|**float**|A média de comandos entregues por segundo.|  
|**delivery_latency**|**int**|A latência entre o comando que insere o banco de dados de distribuição e sendo aplicado ao Assinante. Em milissegundos.|  
|**total_delivered_commands**|**bigint**|O número total de comandos entregues desde que a assinatura foi criada.|  
|**error_id**|**int**|A ID do erro na tabela do sistema **MSrepl_error** .|  
|**updateable_row**|**bit**|Defina como **1** se a linha do histórico puder ser substituída.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
