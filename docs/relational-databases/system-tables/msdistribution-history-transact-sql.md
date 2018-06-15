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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7196fcd36a995b0e1e8feb3f7436d1f634da375c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005933"
---
# <a name="msdistributionhistory-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdistribution_history** tabela contém linhas de histórico para os agentes de distribuição associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**Int**|A ID do Distribution Agent.|  
|**runstatus**|**Int**|O status de execução:<br /><br /> **1** = iniciar.<br /><br /> **2** = êxito.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = repetição.<br /><br /> **6** = falha.|  
|**start_time**|**datetime**|A hora inicial de execução do trabalho.|  
|**time**|**datetime**|A hora de registro da mensagem.|  
|**duration**|**Int**|A duração, em segundos, da sessão de mensagem.|  
|**Comentários**|**nvarchar(4000)**|O texto da mensagem.|  
|**xact_seqno**|**varbinary(16)**|O último número de sequência da transação processado.|  
|**current_delivery_rate**|**float**|O número médio de comandos fornecidos por segundo desde a última entrada de histórico.|  
|**current_delivery_latency**|**Int**|A latência entre o comando que insere o banco de dados de distribuição e o aplicado ao Assinante desde a última entrada de histórico Em milissegundos.|  
|**delivered_transactions**|**Int**|O número total de transações entregues na sessão.|  
|**delivered_commands**|**Int**|O número total de comandos entregues na sessão.|  
|**average_commands**|**Int**|O número médio de comandos entregues na sessão.|  
|**delivery_rate**|**float**|A média de comandos entregues por segundo.|  
|**delivery_latency**|**Int**|A latência entre o comando que insere o banco de dados de distribuição e sendo aplicado ao Assinante. Em milissegundos.|  
|**total_delivered_commands**|**bigint**|O número total de comandos entregues desde que a assinatura foi criada.|  
|**error_id**|**Int**|A ID do erro no **MSrepl_error** tabela do sistema.|  
|**updateable_row**|**bit**|Definido como **1** se a linha de histórico pode ser substituída.|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
