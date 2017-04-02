---
title: "Exibir informa&#231;&#245;es e executar tarefas para os agentes associados a uma publica&#231;&#227;o (Replication Monitor) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "agentes [replicação do SQL Server], exibindo informações"
  - "exibindo informações do agente de replicação"
  - "agentes [replicação do SQL Server], tarefas do Replication Monitor"
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibir informa&#231;&#245;es e executar tarefas para os agentes associados a uma publica&#231;&#227;o (Replication Monitor)
  O Replication Monitor fornece o **agentes** guia, que inclui informações sobre os agentes associados com a publicação selecionada. O Distribution Agent e o agente de mesclagem estão associados com assinaturas; Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
 Essa guia exibe informações sobre os seguintes agentes:  
  
-   O Agente de Instantâneo, que é usado por todas as publicações.  
  
-   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
  
-   O Agente de Leitor de Fila, que é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
 Para exibir mais informações sobre as opções nessa guia, clique em **Ajuda** na barra de menu. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para exibir informações e executar tarefas para os agentes associados com uma publicação  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique o **agentes** guia para exibir informações sobre agentes. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre um agente (como mensagens informativas e mensagens de erro), clique o agente e, em seguida, clique em **Exibir detalhes**.  
  
    -   Para exibir informações detalhadas sobre o trabalho que executa o agente (como a agenda, detalhes de etapa de trabalho e assim por diante), o agente de atalho e, em seguida, clique em **propriedades**.  
  
    -   Para gerenciar os perfis para o agente, clique o agente e, em seguida, clique em **perfil de agente**. Para obter mais informações, consulte [trabalhar com perfis do Replication Agent](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Para iniciar um agente não está em execução, clique o agente e, em seguida, clique em **Iniciar agente**.  
  
    -   Para interromper um agente está em execução, clique o agente e, em seguida, clique em **Parar agente**.  
  
## Consulte também  
 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [Exibir informações e executar tarefas para uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  