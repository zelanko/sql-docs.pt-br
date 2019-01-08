---
title: IHextendedSubscriptionView (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30ba4a0947f98ab34ed8c11ef0e8f3a25c3e453b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756978"
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHextendedSubscriptionView** exibição expõe informações de assinatura de uma publicação não SQL Server. Essa exibição é armazenada na **distribuição** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|O identificador exclusivo para um artigo.|  
|**dest_db**|**sysname**|O nome do banco de dados de destino.|  
|**srvid**|**smallint**|O identificador exclusivo para o Assinante.|  
|**login_name**|**sysname**|O logon usado na conexão com um Assinante.|  
|**distribution_jobid**|**binary**|Identifica um trabalho do Distribution Agent.|  
|**publisher_database_id**|**int**|Identifica o banco de dados de publicação.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = push - o agente de distribuição é executado no assinante.<br /><br /> **1** = pull - o agente de distribuição é executado no distribuidor.|  
|**sync_type**|**tinyint**|O tipo de sincronização inicial:<br /><br /> **1** = automático<br /><br /> **2** = nenhum|  
|**status**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo<br /><br /> **1** = assinado<br /><br /> **2** = ativo|  
|**snapshot_seqno_flag**|**bit**|Indica se um número de sequência de instantâneo está sendo usado.|  
|**independent_agent**|**bit**|Especifica se existe um Distribution Agent autônomo para essa publicação.<br /><br /> **0** = a publicação usa um Distribution Agent compartilhado e cada par publicador/assinante do banco de dados tem um agente compartilhado, único.<br /><br /> **1** = há um Distribution Agent autônomo para essa publicação.|  
|**subscription_time**|**datetime**|Somente para uso interno.|  
|**loopback_detection**|**bit**|Aplica-se a assinaturas que fazem parte de uma topologia de replicação transacional bidirecional. A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **1** = não envia de volta.<br /><br /> **0** = envia de volta.|  
|**agent_id**|**int**|O identificador exclusivo do Distribution Agent.|  
|**update_mode**|**tinyint**|Indica o tipo de modo de atualização, que pode ser um dos seguintes:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.<br /><br /> **2** = atualização na fila usando o enfileiramento de mensagens.<br /><br /> **3** = imediato atualizar com atualização enfileirada como failover usando o enfileiramento de mensagens.<br /><br /> **4** = atualização na fila usando a fila do SQL Server.<br /><br /> **5** = atualização imediata com failover de atualização na fila, usando a fila do SQL Server.|  
|**publisher_seqno**|**varbinary(16)**|O número de sequência da transação no Publicador para esta assinatura.|  
|**ss_cplt_seqno**|**varbinary(16)**|O número de sequência usado para significar a conclusão do processamento de instantâneo simultâneo.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
