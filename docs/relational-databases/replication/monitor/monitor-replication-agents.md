---
title: "Monitorar agentes de replica&#231;&#227;o | Microsoft Docs"
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
  - "monitorando o desempenho [replicação do SQL Server], agentes"
  - "Agente de Leitor de Log, monitorando"
  - "Replication Monitor, agentes"
  - "Agente de Mesclagem, monitorando"
  - "Queue Reader Agent, monitorando"
  - "Agente de Instantâneo, monitorando"
  - "agentes [replicação do SQL Server], monitorando"
  - "Agente de Distribuição, monitorando"
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Monitorar agentes de replica&#231;&#227;o
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Monitor de replicação fornece uma exibição sistemática da atividade de replicação, mas também torna fácil de localizar informações em um agente específico. A lista a seguir inclui cada agente, as guias no Replication Monitor onde pode ser localizado e um link para um tópico que explica como acessar essas guias:  
  
-   Os agentes a seguir estão associados às publicações no Replication Monitor:  
  
    -   Snapshot Agent  
  
    -   Agente de Leitor de Log  
  
    -   Queue Reader Agent  
  
     Acessar informações e tarefas associadas a esses agentes por meio das seguintes guias: **agentes** (disponível para cada publicador e publicação) e **avisos** (disponível para cada publicação). Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   Os agentes a seguir estão associados às assinaturas no Replication Monitor:  
  
    -   Agente de Distribuição  
  
    -   Merge Agent  
  
     Acessar informações e tarefas associadas a esses agentes por meio das seguintes guias: **lista de observação da assinatura** (disponível para cada publicador) ou o **todas as assinaturas** guia (disponível para cada publicação). Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Usando o SQL Server Management Studio para monitorar agentes de replicação  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] Fornece as seguintes caixas de diálogo para monitorar agentes de replicação:  
  
-   **Exibir o Status do Snapshot Agent** (para todas as publicações)  
  
-   **Exibir Status do Log Reader Agent** (para todas as publicações transacionais)  
  
-   **Exibir Status de sincronização** (para todas as assinaturas; essa caixa de diálogo permite acesso ao Distribution Agent e o agente de mesclagem)  
  
 O Replication Monitor fornece informações adicionais sobre cada agente e fornece monitoramento para o Queue Reader Agent, se necessário. Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), e [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
#### Para monitorar o Snapshot Agent e o Log Reader Agent  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Uma publicação de atalho e, em seguida, clique em **Exibir Status do Log Reader Agent** ou **Exibir o Status do Snapshot Agent**.  
  
4.  No **Exibir Status do Log Reader Agent** ou **Exibir o Status do Snapshot Agent** caixa de diálogo:  
  
    -   Exiba o status do agente.  
  
    -   Inicie ou pare o agente, se necessário.  
  
    -   Clique em **Monitor** Iniciar **Replication Monitor**.  
  
5.  Clique em **Fechar**.  
  
#### Para monitorar o Distribution Agent e o Merge Agent (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação para a assinatura que você quer monitorar.  
  
4.  Clique com botão direito a assinatura e, em seguida, clique em **Exibir o Status de sincronização**.  
  
5.  No **Exibir o Status de sincronização** caixa de diálogo:  
  
    -   Exiba o status do agente.  
  
    -   Inicie ou pare o agente, se necessário.  
  
    -   Para assinaturas push, clique em **Monitor** Iniciar **Replication Monitor**.  
  
    -   Para assinaturas pull, clique em **Exibir histórico de trabalho** para iniciar o **Visualizador do arquivo de Log**, que exibe a saída do log do agente.  
  
6.  Clique em **Fechar**.  
  
#### Para monitorar o Distribution Agent e o Merge Agent (no Assinante)  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com botão direito a assinatura que você deseja monitorar e, em seguida, clique em **Exibir o Status de sincronização**.  
  
4.  No **Exibir o Status de sincronização** caixa de diálogo:  
  
    -   Exiba o status do agente.  
  
    -   Inicie ou pare o agente, se necessário.  
  
    -   Clique em **Exibir histórico de trabalho** para iniciar o **Visualizador do arquivo de Log**, que exibe a saída do log do agente.  
  
5.  Clique em **Fechar**.  
  
## Consulte também  
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Visão geral dos agentes de replicação.](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  