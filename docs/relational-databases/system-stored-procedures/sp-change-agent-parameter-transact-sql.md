---
description: sp_change_agent_parameter (Transact-SQL)
title: sp_change_agent_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_parameter_TSQL
- sp_change_agent_parameter
helpviewer_keywords:
- sp_change_agent_parameter
ms.assetid: f1fbecc7-e64f-405c-8067-6b38c1f3c0a0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6020788189dbd352b3a469809e0a95a85a6a5a5f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548253"
---
# <a name="sp_change_agent_parameter-transact-sql"></a>sp_change_agent_parameter (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera um parâmetro de um perfil de agente de replicação armazenado na tabela do sistema [MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) . Esse procedimento armazenado é executado no Distribuidor, onde o agente está sendo executado, ou em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_agent_parameter [ @profile_id= ] profile_id, [ @parameter_name= ] 'parameter_name', [ @parameter_value= ] 'parameter_value'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id,` É a ID do perfil. *profile_id* é **int**, sem padrão.  
  
`[ @parameter_name = ] 'parameter_name'` É o nome do parâmetro. *parameter_name* é **sysname**, sem padrão. Para perfis de sistema, os parâmetros que podem ser alterados dependem do tipo de agente. Para descobrir que tipo de agente esse *profile_id* representa, localize a coluna *profile_id* na tabela **MSagent_profiles** e observe o valor de *agent_type* .  
  
> [!NOTE]  
>  Se um parâmetro tiver suporte para um determinado *agent_type*, mas não tiver sido definido no perfil do agente, um erro será retornado. Para adicionar um parâmetro a um perfil de agente, você deve executar [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md).  
  
 Para um Agente de Instantâneo (*agent_type* = **1**), se definido no perfil, as seguintes propriedades podem ser alteradas:  
  
-   **70Subscribers**  
  
-   **BcpBatchSize**  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxNetworkOptimization**  
  
-   **Saída**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **QueryTimeout**  
  
-   **StartQueueTimeout**  
  
-   **UsePerArticleContentsView**  
  
 Para um Agente de Leitor de Log (*agent_type* = **2**), se definido no perfil, as seguintes propriedades podem ser alteradas:  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MessageInterval**  
  
-   **Saída**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ReadBatchSize**  
  
-   **ReadBatchThreshold**  
  
 Para um agente de distribuição (*agent_type* = **3**), se definido no perfil, as seguintes propriedades podem ser alteradas:  
  
-   **BcpBatchSize**  
  
-   **CommitBatchSize**  
  
-   **CommitBatchThreshold**  
  
-   **FileTransferType**  
  
-   **HistoryVerboseLevel**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDeliveredTransactions**  
  
-   **MessageInterval**  
  
-   **Saída**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **QuotedIdentifier**  
  
-   **SkipErrors**  
  
-   **TransactionsPerHistory**  
  
 Para um agente de mesclagem (*agent_type* = **4**), se definido no perfil, as seguintes propriedades podem ser alteradas:  
  
-   **AltSnapshotFolder**  
  
-   **BcpBatchSize**  
  
-   **ChangesPerHistory**  
  
-   **DestThreads**  
  
-   **DownloadGenerationsPerBatch**  
  
-   **DownloadReadChangesPerBatch**  
  
-   **DownloadWriteChangesPerBatch**  
  
-   **DynamicSnapshotLocation**  
  
-   **ExchangeType**  
  
-   **FastRowCount**  
  
-   **FileTransferType**  
  
-   **GenerationChangeThreshold**  
  
-   **HistoryVerboseLevel**  
  
-   **InputMessageFile**  
  
-   **InteractiveResolution**  
  
-   **InterruptOnMessagePattern**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDownloadChanges**  
  
-   **MaxUploadChanges**  
  
-   **MetadataRetentionCleanup**  
  
-   **NumDeadlockRetries**  
  
-   **Saída**  
  
-   **OutputMessageFile**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **ParallelUploadDownload**  
  
-   **PauseOnMessagePattern**  
  
-   **PauseTime**  
  
-   **PollingInterval**  
  
-   **ProcessMessagesAtPublisher**  
  
-   **ProcessMessagesAtSubscriber**  
  
-   **QueryTimeout**  
  
-   **QueueSizeMultiplier**  
  
-   **SrcThreads**  
  
-   **StartQueueTimeout**  
  
-   **SyncToAlternate**  
  
-   **UploadGenerationsPerBatch**  
  
-   **UploadReadChangesPerBatch**  
  
-   **UploadWriteChangesPerBatch**  
  
-   **UseInprocLoader**  
  
-   **Validar**  
  
-   **ValidateInterval**  
  
 Para um Queue Reader Agent (*agent_type* = **9**), se definido no perfil, as seguintes propriedades podem ser alteradas:  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **Saída**  
  
-   **OutputVerboseLevel**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ResolverState**  
  
-   **SQLQueueMode**  
  
 Para ver quais parâmetros foram definidos para um determinado perfil, execute **sp_help_agent_profile** e observe a *profile_name* associada ao *profile_id*. Com o *profile_id*apropriado, a próxima execução **sp_help_agent_parameters** usando essa *profile_id* para ver os parâmetros associados ao perfil. Os parâmetros podem ser adicionados a um perfil executando [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md).  
  
`[ @parameter_value = ] 'parameter_value'` É o novo valor do parâmetro. *parameter_value* é **nvarchar (255)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_change_agent_parameter** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_change_agent_parameter**.  
  
## <a name="see-also"></a>Consulte Também  
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [&#41;&#40;Transact-SQL de sp_add_agent_parameter ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_drop_agent_parameter ](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_agent_parameter ](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
