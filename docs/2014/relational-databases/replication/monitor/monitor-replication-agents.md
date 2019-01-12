---
title: Monitorar os agentes de replicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab277c5ad8d85fdc7c24046bfa191078525fe705
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132306"
---
# <a name="monitor-replication-agents"></a>Monitorar agentes de replicação
  O[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor fornece uma exibição sistemática da atividade de replicação, mas também torna direta a localização de informações em um agente específico. A lista a seguir inclui cada agente, as guias no Replication Monitor onde pode ser localizado e um link para um tópico que explica como acessar essas guias:  
  
-   Os agentes a seguir estão associados às publicações no Replication Monitor:  
  
    -   Snapshot Agent  
  
    -   Agente de Leitor de Log  
  
    -   Queue Reader Agent  
  
     Informações de acesso e as tarefas associadas a esses agentes por meio de guias a seguir: **Agentes** (disponível para cada publicador e publicação) e **avisos** (disponível para cada publicação). Para obter mais informações, consulte [exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).  
  
-   Os agentes a seguir estão associados às assinaturas no Replication Monitor:  
  
    -   Agente de Distribuição  
  
    -   Merge Agent  
  
     Informações de acesso e as tarefas associadas a esses agentes por meio de guias a seguir: **Lista de observação da assinatura** (disponível para cada publicador) ou o **todas as assinaturas** guia (disponível para cada publicação). Para obter mais informações, consulte [exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="using-sql-server-management-studio-to-monitor-replication-agents"></a>Usando o SQL Server Management Studio para monitorar agentes de replicação  
 O[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] fornece as seguintes caixas de diálogo para monitorar agentes de replicação:  
  
-   **Exibir Status do Snapshot Agent** (para todas as publicações)  
  
-   **Exibir Status do Log Reader Agent** (para todas as publicações transacionais)  
  
-   **Exibir Status da Sincronização** (para todas as assinaturas; essa caixa de diálogo permite acesso ao Distribution Agent e ao Merge Agent)  
  
 O Replication Monitor fornece informações adicionais sobre cada agente e fornece monitoramento para o Queue Reader Agent, se necessário. Para obter mais informações, consulte [exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).  
  
#### <a name="to-monitor-the-snapshot-agent-and-log-reader-agent"></a>Para monitorar o Snapshot Agent e o Log Reader Agent  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse em uma publicação e, então, clique em **Exibir Status do Log Reader Agent** ou **Exibir Status do Snapshot Agent**.  
  
4.  Na caixa de diálogo do **Exibir Status do Log Reader Agent** ou do **Exibir Status do Snapshot Agent** :  
  
    -   Exiba o status do agente.  
  
    -   Inicie ou pare o agente, se necessário.  
  
    -   Clique em **Monitor** para iniciar o **Replication Monitor**.  
  
5.  Clique em **Fechar**.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-publisher"></a>Para monitorar o Distribution Agent e o Merge Agent (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
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
 [Monitorando a Replicação](../monitoring-replication.md)   
 [Visão geral dos agentes de replicação](../agents/replication-agents-overview.md)  
  
  
