---
description: MSlogreader_history (Transact-SQL)
title: MSlogreader_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSlogreader_history_TSQL
- MSlogreader_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_history system table
ms.assetid: 2e399fa1-3591-4c1c-96b7-7964fe82c7c4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae2abdcaf4014df405ebf6dcefff8e2207530a93
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545719"
---
# <a name="mslogreader_history-transact-sql"></a>MSlogreader_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSlogreader_history** contém linhas de histórico para os agentes de leitor de log associados ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do Log Reader Agent.|  
|**runstatus**|**int**|O status da execução:<br /><br /> 1 = Iniciar.<br /><br /> 2 = Êxito.<br /><br /> 3 = Em andamento.<br /><br /> 4 = Inativo.<br /><br /> 5 = Repetir.<br /><br /> 6 = Falha.|  
|**start_time**|**datetime**|A hora inicial de execução do trabalho.|  
|**time**|**datetime**|A hora de registro da mensagem.|  
|**duration**|**int**|A duração, em segundos, da sessão de mensagem.|  
|**feitos**|**nvarchar(255)**|O texto de mensagem.|  
|**xact_seqno**|**varbinary(16)**|O último número de sequência da transação processado.|  
|**delivery_time**|**int**|A hora de entrega da primeira transação.|  
|**delivered_transactions**|**int**|O número total de transações entregues na sessão.|  
|**delivered_commands**|**int**|O número total de comandos entregues na sessão.|  
|**average_commands**|**int**|O número médio de comandos entregues na sessão.|  
|**delivery_rate**|**float**|A média de comandos entregues por segundo.|  
|**delivery_latency**|**int**|A latência entre o comando que insere o banco de dados publicado e sendo inserido no banco de dados de distribuição. Em milissegundos.|  
|**error_id**|**int**|A ID do erro na tabela do sistema **MSrepl_error** .|  
|**timestamp**|**timestamp**|A coluna de carimbo de data e hora dessa tabela.|  
|**updateable_row**|**bit**|Defina como **1** se a linha do histórico puder ser substituída.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
