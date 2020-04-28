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
ms.openlocfilehash: 8f080f5defd5143d3822e86eeeb3c7242b51d08d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029575"
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A exibição **IHextendedSubscriptionView** expõe informações sobre assinatura para uma publicação não SQL Server. Essa exibição é armazenada no banco de dados de **distribuição** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|O identificador exclusivo para um artigo.|  
|**dest_db**|**sysname**|O nome do banco de dados de destino.|  
|**srvid**|**smallint**|O identificador exclusivo para o Assinante.|  
|**login_name**|**sysname**|O logon usado na conexão com um Assinante.|  
|**distribution_jobid**|**binary**|Identifica um trabalho do Distribution Agent.|  
|**publisher_database_id**|**int**|Identifica o banco de dados de publicação.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = push-o Distribution Agent é executado no Assinante.<br /><br /> **1** = pull-o Distribution Agent é executado no distribuidor.|  
|**sync_type**|**tinyint**|O tipo de sincronização inicial:<br /><br /> **1** = automático<br /><br /> **2** = nenhum|  
|**status**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo<br /><br /> **1** = assinado<br /><br /> **2** = ativo|  
|**snapshot_seqno_flag**|**bit**|Indica se um número de sequência de instantâneo está sendo usado.|  
|**independent_agent**|**bit**|Especifica se existe um Distribution Agent autônomo para essa publicação.<br /><br /> **0** = a publicação usa um agente de distribuição compartilhado e cada par de banco de dados/assinante do Publicador tem um agente único e compartilhado.<br /><br /> **1** = há um agente de distribuição autônomo para esta publicação.|  
|**subscription_time**|**datetime**|Somente para uso interno.|  
|**loopback_detection**|**bit**|Aplica-se a assinaturas que fazem parte de uma topologia de replicação transacional bidirecional. A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **1** = não envia de volta.<br /><br /> **0** = envia de volta.|  
|**agent_id**|**int**|O identificador exclusivo do Distribution Agent.|  
|**update_mode**|**tinyint**|Indica o tipo de modo de atualização, que pode ser um dos seguintes:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.<br /><br /> **2** = atualização em fila usando o enfileiramento de mensagens.<br /><br /> **3** = atualização imediata com atualização em fila como failover usando o enfileiramento de mensagens.<br /><br /> **4** = atualização em fila usando a fila de SQL Server.<br /><br /> **5** = atualização imediata com failover de atualização em fila, usando SQL Server fila.|  
|**publisher_seqno**|**varbinary(16)**|O número de sequência da transação no Publicador para esta assinatura.|  
|**ss_cplt_seqno**|**varbinary(16)**|O número de sequência usado para significar a conclusão do processamento de instantâneo simultâneo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogêneo](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
