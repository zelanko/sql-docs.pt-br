---
title: Perfis do agente de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, profiles
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- Merge Agent, profiles
- agents [SQL Server replication], profiles
- Queue Reader Agent, profiles
- profiles [SQL Server], replication agents
- Snapshot Agent, profiles
- Log Reader Agent, profiles
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a752b21460c2dd337d12ee43acdd981dadd4335b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76288257"
---
# <a name="replication-agent-profiles"></a>Perfis do Agente de Replicação
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Um conjunto de perfis de agente é instalado no distribuidor quando a replicação é configurada. Um perfil de agente contém um conjunto de parâmetros que são usados sempre que um agente é executado: cada agente faz logon no distribuidor durante seu processo de inicialização e consulta os parâmetros em seu perfil. Para assinaturas de mesclagem que usam sincronização da Web, os perfis são baixados e armazenados no assinante. Se o perfil for alterado, o perfil no assinante será atualizado na próxima vez que o Agente de Mesclagem for executado. Para obter mais informações sobre a sincronização da Web, consulte [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 A replicação fornece um perfil padrão para cada agente e perfis adicionais predefinidos para o Log Reader Agent, o Distribution Agent e o Merge Agent. Além dos perfis fornecidos, você pode criar perfis adaptados às exigências de seu aplicativo. Um perfil de agente permite alterar, facilmente, parâmetros fundamentais para todos os agentes associados àquele perfil. Por exemplo, se você tem 20 Agente de Instantâneos e precisa alterar o valor do tempo limite de consulta (parâmetro **-QueryTimeout** ), você pode atualizar o perfil utilizado pelos Agentes de Instantâneo e todos os agentes desse tipo usarão o novo valor automaticamente na próxima vez que forem executados.  
  
 Você também pode ter perfis diferentes para instâncias diferentes de um agente. Por exemplo, um Agente de Mesclagem que se conecta ao Publicador e ao Distribuidor por meio de uma conexão discada poderá usar um conjunto de parâmetros mais adequados para links de comunicações mais lentas usando o perfil **vínculo lento** .  
  
> [!NOTE]  
>  Se você especificar um valor para o parâmetro de um agente na linha de comando, esse valor substitui o valor definido para o mesmo parâmetro no perfil do agente.  
  
 **Para usar e modificar perfis de agente**  
  
-   [Trabalhar com perfis do Agente de Replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
## <a name="snapshot-agent-profiles"></a>Perfis do Agente de Instantâneo  
 A tabela abaixo mostra os parâmetros definidos no perfil padrão para o Agente de Instantâneo. Para obter mais informações sobre esses parâmetros, consulte [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md).  
  
||padrão|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## <a name="log-reader-agent-profiles"></a>Perfis do Log Reader Agent  
 A tabela abaixo mostra os parâmetros definidos nos perfis para o Log Reader Agent. Cada coluna na tabela representa um perfil nomeado. Para obter mais informações sobre esses parâmetros, consulte [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
||padrão|histórico detalhado|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|1|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## <a name="distribution-agent-profiles"></a>Perfis do Distribution Agent  
 A tabela abaixo mostra os parâmetros definidos nos perfis para o Distribution Agent. Cada coluna na tabela representa um perfil nomeado. Para obter mais informações sobre esses parâmetros, consulte [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
||padrão|histórico detalhado|Gerenciador de Sincronização do Windows|Continuar em erros de consistência de dados|Perfil de distribuição para fluxo contínuo do banco de dados OLE|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1000|1000|1000|1000|1000|  
|**-HistoryVerboseLevel**|1|2|1|1|1|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|1|1|1|1|1|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULO|NULO|NULO|NULO|32768|  
|**-PacketSize**|NULO|NULO|NULO|NULO|32768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULO|NULO|NULO|**-SkipErrors** 2601:2627:20598|NULO|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULO|NULO|NULO|NULO|**-UseOledbStreaming**|  
  
## <a name="merge-agent-profiles"></a>Perfis do Merge Agent  
 A tabela abaixo mostra os parâmetros definidos nos perfis para o Merge Agent. Cada coluna na tabela representa um perfil nomeado. Para obter mais informações sobre esses parâmetros, consulte [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
||padrão|histórico detalhado|Gerenciador de Sincronização do Windows|validação do número de linhas.|validação do número de linhas e da soma de verificação|vínculo lento|servidor a servidor de alto volume|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1000|  
|**-DestThreads**|2|1|1|1|1|1|4|  
|**-DownloadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-DownloadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-DownloadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-FastRowCount**|1|1|1|1|1|1|1|  
|**-HistoryVerboseLevel**|2|3|1|1|2|1|2|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|15|15|  
|**-MaxDownloadChanges**|0|0|0|0|0|0|0|  
|**-MaxUploadChanges**|0|0|0|0|0|0|0|  
|**-MetadataRetentionCleanup**|1|1|1|1|1|1|1|  
|**-NumDeadlockRetries**|5|5|5|5|5|5|5|  
|**-ParallelUploadDownload**|NULO|NULO|NULO|NULO|NULO|NULO|1|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULO|NULO|NULO|NULO|NULO|NULO|5|  
|**-SrcThreads**|2|2|2|2|2|1|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|1|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## <a name="queue-reader-agent-profiles"></a>Perfis do Queue Reader Agent  
 A tabela abaixo mostra os parâmetros definidos no perfil padrão para o Queue Reader Agent. Para obter mais informações sobre esses parâmetros, consulte [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md).  
  
||padrão|  
|-|-------------|  
|**-HistoryVerboseLevel**|1|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Exibir e modificar parâmetros do prompt de comando do agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)   
 [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
