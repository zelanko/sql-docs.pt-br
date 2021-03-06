---
description: MSsubscription_agents (Transact-SQL)
title: MSsubscription_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e92e0e3476aa377577d00fca63a8348c47d09002
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540844"
---
# <a name="mssubscription_agents-transact-sql"></a>MSsubscription_agents (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSsubscription_agents** é usada por agente de distribuição e gatilhos de assinaturas atualizáveis para rastrear Propriedades de assinatura. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID da linha.|  
|**programa**|**sysname**|O nome do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**documento**|**sysname**|O nome da publicação.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> 0 = Push.<br /><br /> 1 = Pull<br /><br /> 2 = Anônimo pull.|  
|**queue_id**|**sysname**|A ID da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fila de mensagens no Publicador. *queue_id* é definido como **SQL** para atualização em fila baseada em SQL.|  
|**update_mode**|**tinyint**|O tipo de atualização:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.<br /><br /> **2** = atualização em fila usando o enfileiramento de mensagens.<br /><br /> **3** = atualização imediata com atualização em fila como failover usando o enfileiramento de mensagens.<br /><br /> **4** = atualização em fila usando a fila de SQL Server.<br /><br /> **5** = atualização imediata com failover de atualização em fila, usando SQL Server fila.|  
|**failover_mode**|**bit**|Se um tipo de failover de atualização tiver sido selecionado, este será o tipo de failover escolhido:<br /><br /> **0** = atualização imediata está sendo usada. Failover não habilitado.<br /><br /> **1** = a atualização em fila está sendo usada. Failover habilitado. A fila que está sendo usada para failover é especificada no valor *update_mode* .|  
|**spid**|**int**|A ID de processo do sistema para a conexão usada pelo Distribution Agent em execução no momento ou executado anteriormente.|  
|**login_time**|**datetime**|A data e a hora da conexão do Distribution Agent em execução no momento ou executado anteriormente.|  
|**allow_subscription_copy**|**bit**|Especifica se a capacidade ou não de copiar banco de dados de assinatura é permitida.|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary(16)**|O identificador exclusivo que representa a versão de uma assinatura anexada.|  
|**last_sync_status**|**int**|O último status de execução do Distribution Agent em execução no momento ou executado anteriormente. Os status podem ser:<br /><br /> **1** = iniciado.<br /><br /> **2** = com êxito.<br /><br /> **3** = em andamento.<br /><br /> **4** = ocioso.<br /><br /> **5** = tentar novamente.<br /><br /> **6** = falha.|  
|**last_sync_summary**|**sysname**|A última mensagem do Distribution Agent em execução no momento ou executado anteriormente. Os status podem ser:<br /><br /> **Iniciais.**<br /><br /> **Foi.**<br /><br /> **Em andamento.**<br /><br /> **Ocioso.**<br /><br /> **Repita.**<br /><br /> **Recuperação.**|  
|**last_sync_time**|**datetime**|A data e a hora em que as colunas *last_sync_summary* e *last_sync_status* foram atualizadas. Agentes de distribuição pull ou anônimos que executam trabalhos do Serviço SqlServer Agent não atualizam essas colunas. Nesse caso, as informações de histórico são registradas na tabela de histórico de trabalho.|  
|**queue_server**|**sysname**|Somente para uso interno.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppullsubscription ](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
