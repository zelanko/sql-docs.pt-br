---
title: "Exibir o status da publica&#231;&#227;o e da assinatura no Replication Monitor | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agente de Leitor de Log, monitorando"
  - "Agente de Mesclagem, monitorando"
  - "Queue Reader Agent, monitorando"
  - "publicações [replicação do SQL Server], exibindo informações"
  - "Agente de Instantâneo, monitorando"
  - "Agente de Distribuição, monitorando"
  - "monitorando o desempenho [replicação do SQL Server], status da publicação"
  - "monitorando o desempenho [replicação do SQL Server], status da assinatura"
  - "assinaturas [replicação do SQL Server], exibindo o status"
  - "Replication Monitor, status da publicação e da assinatura"
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Exibir o status da publica&#231;&#227;o e da assinatura no Replication Monitor
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor exibe informações de status para publicações e inscrições:  
  
-   O status de uma publicação é determinado pelo status de prioridade mais alta de suas assinaturas. Por exemplo, se uma assinatura para uma publicação tiver um erro e outra tiver um problema de desempenho, será exibido um status de erro para a publicação.  
  
-   O status de uma assinatura é determinado pelo status dos agentes que servem à assinatura. Para a replicação de mesclagem, esse é o Merge Agent. Para a replicação transacional, esse é o Log Reader Agent ou o Distribution Agent (é exibido o status com maior prioridade; o status também pode ser determinado pelo Queue Reader Agent, se forem usadas assinaturas de atualização em fila). Para replicação de instantâneo, esse é o Snapshot Agent ou o Distribution Agent (é exibido o status com maior prioridade).  
  
 As tabelas nas seções a seguir, listam os possíveis valores de status para publicações e assinaturas. Três dos valores de status só serão exibidos caso um limite seja atingido ou excedido:  
  
-   Assinatura perdendo a validade  
  
     Esse valor de status se aplica a todos os tipos de replicação. Para obter mais informações, consulte [definir limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Desempenho crítico  
  
     Esse valor de status se aplica à replicação transacional e à replicação de mesclagem. Para obter mais informações, consulte [monitorar o desempenho com o Replication Monitor](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
-   Mesclagem de execução longa  
  
     Esse valor de status se aplica à replicação de mesclagem. Para obter mais informações, consulte [monitorar o desempenho com o Replication Monitor](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 Além dos status da publicação e da assinatura, a replicação de mesclagem fornece estatísticas em nível de artigo, que fornecem informações detalhadas sobre: quanto tempo mais a fase de mesclagem demorará para terminar; quanto tempo foi gasto no processamento de um determinado artigo; o tipo de conexão que um Assinante está usando; e outras informações importantes. As estatísticas são exibidas na janela Merge Agent no Replication Monitor. As replicações de instantâneo e transacional fornecem informações detalhadas sobre o processamento do Distribution Agent.  
  
 **Para exibir o status da publicação e da assinatura**  
  
-   Monitor de replicação: [Exibir informações e executar tarefas para uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md) e [Exibir informações e executar tarefas para uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
  
 **Para exibir informações detalhadas para os agentes**  
  
-   Monitor de replicação: [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md) e [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Valores de status da publicação  
 A tabela abaixo mostra os valores de status da publicação e seus ícones correspondentes em ordem de prioridade.  
  
|Status|Ícone|  
|------------|----------|  
|Erro|![Ícone de IU: erro](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Ícone de IU: erro")|  
|Desempenho crítico|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Tentando novamente comando com falha|![Ícone de IU: repetição do agente de replicação](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Ícone de IU: repetição do agente de replicação")|  
|OK|none|  
  
## Valores de status da assinatura  
 As tabelas abaixo mostram os valores de status da assinatura e seus ícones correspondentes em ordem de prioridade. É possível que uma assinatura para ser em dois estados ao mesmo tempo, como **expirando em breve/expirado** e **repetindo falha no comando**; o status de prioridade mais alto é exibido.  
  
 Os valores de status **desempenho crítico**, **expirando em breve/expirado**, e **não inicializado** são avisos. Quando é exibido um aviso, o Replication Monitor também exibe se um agente está sendo executado. Por exemplo, o status poderia ser **Executando, Desempenho crítico**.  
  
### Assinaturas transacionais  
  
|Status|Ícone|  
|------------|----------|  
|Erro|![Ícone de IU: erro](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Ícone de IU: erro")|  
|Desempenho crítico|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Expirando em breve/Expirado|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Assinatura não inicializada|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Tentando novamente comando com falha|![Ícone de IU: repetição do agente de replicação](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Ícone de IU: repetição do agente de replicação")|  
|Não está sendo executado|![Ícone de IU: agente de replicação interrompido](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "Ícone de IU: agente de replicação interrompido")|  
|Executando|![Ícone de IU: agente de replicação em execução](../../../relational-databases/replication/monitor/media/repl-icon-running.png "Ícone de IU: agente de replicação em execução")|  
  
### Assinaturas de mesclagem  
  
|Status|Ícone|  
|------------|----------|  
|Erro|![Ícone de IU: erro](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Ícone de IU: erro")|  
|Desempenho crítico|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Mesclagem de execução longa|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Expirando em breve/Expirado|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Assinatura não inicializada|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Tentando novamente comando com falha|![Ícone de IU: repetição do agente de replicação](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Ícone de IU: repetição do agente de replicação")|  
|Sincronizando|![Ícone de IU: agente de replicação em execução](../../../relational-databases/replication/monitor/media/repl-icon-running.png "Ícone de IU: agente de replicação em execução")|  
|Não sincronizando|![Ícone de IU: agente de replicação interrompido](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "Ícone de IU: agente de replicação interrompido")|  
  
### Assinaturas de instantâneo  
  
|Status|Ícone|  
|------------|----------|  
|Erro|![Ícone de IU: erro](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "Ícone de IU: erro")|  
|Expirando em breve/Expirado|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Assinatura não inicializada|![Ícone de IU: aviso](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "Ícone de IU: aviso")|  
|Tentando novamente comando com falha|![Ícone de IU: repetição do agente de replicação](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "Ícone de IU: repetição do agente de replicação")|  
|Sincronizando|![Ícone de IU: agente de replicação em execução](../../../relational-databases/replication/monitor/media/repl-icon-running.png "Ícone de IU: agente de replicação em execução")|  
|Não sincronizando|![Ícone de IU: agente de replicação interrompido](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "Ícone de IU: agente de replicação interrompido")|  
  
## Consulte também  
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  