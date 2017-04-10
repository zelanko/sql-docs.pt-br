---
title: "Perfis do Agente de Replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agente de Distribuição, perfis"
  - "replicação [SQL Server], agentes e perfis"
  - "perfis de agente de replicação [SQL Server]"
  - "Agente de Mesclagem, perfis"
  - "agentes [replicação do SQL Server], perfis"
  - "Queue Reader Agent, perfis"
  - "perfis [SQL Server], agentes de replicação"
  - "Agente de Instantâneo, perfis"
  - "Agente de Leitor de Log, perfis"
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Perfis do Agente de Replica&#231;&#227;o
  Um conjunto de perfis de agente é instalado no distribuidor quando a replicação é configurada. Um perfil de agente contém um conjunto de parâmetros que são usados sempre que um agente é executado: cada agente faz logon no distribuidor durante seu processo de inicialização e consulta os parâmetros em seu perfil. Para assinaturas de mesclagem que usam sincronização da Web, os perfis são baixados e armazenados no assinante. Se o perfil for alterado, o perfil no assinante será atualizado na próxima vez que o Agente de Mesclagem for executado. Para obter mais informações sobre a sincronização da Web, consulte [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 A replicação fornece um perfil padrão para cada agente e perfis adicionais predefinidos para o Log Reader Agent, o Distribution Agent e o Merge Agent. Além dos perfis fornecidos, você pode criar perfis adaptados às exigências de seu aplicativo. Um perfil de agente permite alterar, facilmente, parâmetros fundamentais para todos os agentes associados àquele perfil. Por exemplo, se você tiver 20 agentes de instantâneo e precisa alterar o valor de tempo limite de consulta (o **- QueryTimeout** parâmetro), você pode atualizar o perfil usado pelos agentes de instantâneo e todos os agentes desse tipo começarão a usar o novo valor automaticamente na próxima vez em que eles são executados.  
  
 Você também pode ter perfis diferentes para instâncias diferentes de um agente. Por exemplo, um agente de mesclagem que se conecta ao publicador e distribuidor através de uma conexão dial-up pode usar um conjunto de parâmetros que são mais adequados para o link de comunicações mais lento usando o **link lento** perfil.  
  
> [!NOTE]  
>  Se você especificar um valor para o parâmetro de um agente na linha de comando, esse valor substitui o valor definido para o mesmo parâmetro no perfil do agente.  
  
 **Para usar e modificar perfis de agente**  
  
-   [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
## Perfis do Agente de Instantâneo  
 A tabela abaixo mostra os parâmetros definidos no perfil padrão para o Agente de Instantâneo. Para obter mais informações sobre esses parâmetros, consulte [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md).  
  
||padrão|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## Perfis do Log Reader Agent  
 A tabela abaixo mostra os parâmetros definidos nos perfis para o Log Reader Agent. Cada coluna na tabela representa um perfil nomeado. Para obter mais informações sobre esses parâmetros, consulte [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
||padrão|histórico detalhado|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|1|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## Perfis do Distribution Agent  
 A tabela abaixo mostra os parâmetros definidos nos perfis para o Distribution Agent. Cada coluna na tabela representa um perfil nomeado. Para obter mais informações sobre esses parâmetros, consulte [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
||padrão|histórico detalhado|Gerenciador de Sincronização do Windows|Continuar em erros de consistência de dados|Perfil de distribuição para fluxo contínuo do banco de dados OLE|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1.000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1.000|1.000|1.000|1.000|1.000|  
|**-HistoryVerboseLevel**|1|2|1|1|1|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|1|1|1|1|1|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULL|NULL|NULL|NULL|32768|  
|**-PacketSize**|NULL|NULL|NULL|NULL|32768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULL|NULL|NULL|**-SkipErrors** 2601:2627:20598|NULL|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULL|NULL|NULL|NULL|**-UseOledbStreaming**|  
  
## Perfis do Merge Agent   
 A tabela abaixo mostra os parâmetros definidos nos perfis para o Merge Agent. Cada coluna na tabela representa um perfil nomeado. Para obter mais informações sobre esses parâmetros, consulte [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
||padrão|histórico detalhado|Gerenciador de Sincronização do Windows|validação do número de linhas.|validação do número de linhas e da soma de verificação|vínculo lento|servidor a servidor de alto volume|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1.000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1.000|  
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
|**-ParallelUploadDownload**|NULL|NULL|NULL|NULL|NULL|NULL|1|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULL|NULL|NULL|NULL|NULL|NULL|5|  
|**-SrcThreads**|2|2|2|2|2|1|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|1|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## Perfis do Queue Reader Agent  
 A tabela abaixo mostra os parâmetros definidos no perfil padrão para o Queue Reader Agent. Para obter mais informações sobre esses parâmetros, consulte [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md).  
  
||padrão|  
|-|-------------|  
|**-HistoryVerboseLevel**|1|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## Consulte também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Exibir e modificar parâmetros de Prompt de comando do agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)   
 [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  