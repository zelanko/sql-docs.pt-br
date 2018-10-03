---
title: MSsubscription_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4be8f754dce7863575721996a9a039b7a3686e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670114"
---
# <a name="mssubscriptionagents-transact-sql"></a>MSsubscription_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsubscription_agents** tabela é usada pelo Distribution Agent e gatilhos de assinaturas atualizáveis para controlar propriedades de assinatura. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID da linha.|  
|**publisher**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> 0 = Push.<br /><br /> 1 = Pull<br /><br /> 2 = Anônimo pull.|  
|**queue_id**|**sysname**|A ID do [!INCLUDE[msCoName](../../includes/msconame-md.md)] fila no publicador de mensagem. *queue_id* é definido como **SQL** para SQL-base de atualização na fila.|  
|**update_mode**|**tinyint**|O tipo de atualização:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.<br /><br /> **2** = atualização na fila usando o enfileiramento de mensagens.<br /><br /> **3** = imediato atualizar com atualização enfileirada como failover usando o enfileiramento de mensagens.<br /><br /> **4** = atualização na fila usando a fila do SQL Server.<br /><br /> **5** = atualização imediata com failover de atualização na fila, usando a fila do SQL Server.|  
|**failover_mode**|**bit**|Se um tipo de failover de atualização tiver sido selecionado, este será o tipo de failover escolhido:<br /><br /> **0** = imediato atualização está sendo usada. Failover não habilitado.<br /><br /> **1** = enfileirada atualização está sendo usada. Failover habilitado. A fila que está sendo usada para failover é especificada na *update_mode* valor.|  
|**spid**|**int**|A ID de processo do sistema para a conexão usada pelo Distribution Agent em execução no momento ou executado anteriormente.|  
|**login_time**|**datetime**|A data e a hora da conexão do Distribution Agent em execução no momento ou executado anteriormente.|  
|**allow_subscription_copy**|**bit**|Especifica se a capacidade ou não de copiar banco de dados de assinatura é permitida.|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary(16)**|O identificador exclusivo que representa a versão de uma assinatura anexada.|  
|**last_sync_status**|**int**|O último status de execução do Distribution Agent em execução no momento ou executado anteriormente. Os status podem ser:<br /><br /> **1** = iniciado.<br /><br /> **2** = foi bem-sucedida.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = repetição.<br /><br /> **6** = falha.|  
|**last_sync_summary**|**sysname**|A última mensagem do Distribution Agent em execução no momento ou executado anteriormente. Os status podem ser:<br /><br /> **Iniciado.**<br /><br /> **Foi bem-sucedida.**<br /><br /> **Em andamento.**<br /><br /> **Ocioso.**<br /><br /> **Tente novamente.**<br /><br /> **Falhe.**|  
|**last_sync_time**|**datetime**|A data e hora em que o *last_sync_summary* e *last_sync_status* colunas foram atualizadas. Agentes de distribuição pull ou anônimos que executam trabalhos do Serviço SqlServer Agent não atualizam essas colunas. Nesse caso, as informações de histórico são registradas na tabela de histórico de trabalho.|  
|**queue_server**|**sysname**|Somente para uso interno.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
