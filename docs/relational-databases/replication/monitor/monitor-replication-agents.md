---
title: "Monitorar os agentes de replicação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], agents
- Log Reader Agent, monitoring
- Replication Monitor, agents
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- agents [SQL Server replication], monitoring
- Distribution Agent, monitoring
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfb5c65e0979e3b28b994c3ec706e092e7c0e0b5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="monitor-replication-agents"></a>Monitorar agentes de replicação
  O[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor fornece uma exibição sistemática da atividade de replicação, mas também torna direta a localização de informações em um agente específico. A lista a seguir inclui cada agente, as guias no Replication Monitor onde pode ser localizado e um link para um tópico que explica como acessar essas guias:  
  
-   Os agentes a seguir estão associados às publicações no Replication Monitor:  
  
    -   Snapshot Agent  
  
    -   Agente de Leitor de Log  
  
    -   Queue Reader Agent  
  
     Acesse as informações e as tarefas associadas a esses agentes por meio das seguintes guias: **Agentes** (disponível para cada Publicador e publicação) e **Avisos** (disponível para cada publicação). Para mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   Os agentes a seguir estão associados às assinaturas no Replication Monitor:  
  
    -   Agente de Distribuição  
  
    -   Agente de Mesclagem  
  
     Acesse as informações e as tarefas associadas a esses agentes por meio das seguintes guias: **Lista de Observação da Assinatura** (disponível para cada Publicador) ou a guia **Todas as Assinaturas** (disponível para cada publicação). Para obter mais informações, consulte [View Information and Perform Tasks for the Agents Associated With a Subscription &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md) [Exibir informações e executar tarefas para os agentes associados a uma assinatura (Replication Monitor)].  
  
## <a name="using-sql-server-management-studio-to-monitor-replication-agents"></a>Usando o SQL Server Management Studio para monitorar agentes de replicação  
 O[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] fornece as seguintes caixas de diálogo para monitorar agentes de replicação:  
  
-   **Exibir Status do Snapshot Agent** (para todas as publicações)  
  
-   **Exibir Status do Log Reader Agent** (para todas as publicações transacionais)  
  
-   **Exibir Status da Sincronização** (para todas as assinaturas; essa caixa de diálogo permite acesso ao Distribution Agent e ao Merge Agent)  
  
 O Replication Monitor fornece informações adicionais sobre cada agente e fornece monitoramento para o Queue Reader Agent, se necessário. Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md), [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md) e [Exibir informações e executar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
#### <a name="to-monitor-the-snapshot-agent-and-log-reader-agent"></a>Para monitorar o Snapshot Agent e o Log Reader Agent  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse em uma publicação e, então, clique em **Exibir Status do Log Reader Agent** ou **Exibir Status do Snapshot Agent**.  
  
4.  Na caixa de diálogo do **Exibir Status do Log Reader Agent** ou do **Exibir Status do Snapshot Agent** :  
  
    -   Exiba o status do agente.  
  
    -   Inicie ou pare o agente, se necessário.  
  
    -   Clique em **Monitor** para iniciar o **Replication Monitor**.  
  
5.  Clique em **Fechar**.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-publisher"></a>Para monitorar o Distribution Agent e o Merge Agent (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação para a assinatura que você quer monitorar.  
  
4.  Clique com o botão direito do mouse na assinatura e clique em **Exibir Status da Sincronização**.  
  
5.  Na caixa de diálogo **Exibir Status da Sincronização** :  
  
    -   Exiba o status do agente.  
  
    -   Inicie ou pare o agente, se necessário.  
  
    -   Para assinaturas push, clique em **Monitor** para iniciar o **Replication Monitor**.  
  
    -   Para assinaturas pull, clique em **Exibir Histórico de Trabalhos** para iniciar o **Visualizador do Arquivo de Log**que exibe a saída do log do agente.  
  
6.  Clique em **Fechar**.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-subscriber"></a>Para monitorar o Distribution Agent e o Merge Agent (no Assinante)  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito do mouse na assinatura que deseja monitorar e clique em **Exibir Status da Sincronização**.  
  
4.  Na caixa de diálogo **Exibir Status da Sincronização** :  
  
    -   Exiba o status do agente.  
  
    -   Inicie ou pare o agente, se necessário.  
  
    -   Clique em **Exibir Histórico do Agente** para iniciar o **Visualizador do Arquivo de Log**que exibe a saída do log do agente.  
  
5.  Clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Replication Agents Overview](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
