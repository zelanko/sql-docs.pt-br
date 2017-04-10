---
title: "Snapshot Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.snapshotagent.f1"
helpviewer_keywords: 
  - "caixa de diálogo Snapshot Agent"
ms.assetid: b715e621-2cd5-4a15-8f58-a341aa8ef5e4
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Snapshot Agent
  O **do Snapshot Agent** caixa de diálogo exibe informações detalhadas sobre o Snapshot Agent, incluindo status, histórico, mensagens informativas e qualquer mensagem de erro.  
  
## Opções  
 Selecione as sessões do Snapshot Agent para exibir do **exibição** menu e, em seguida, selecione uma sessão específica na grade rotulada **sessões do Snapshot Agent**. Informações detalhadas sobre essa sessão são exibidas na grade rotulada **Ações na sessão selecionada**. Se a sessão selecionada terminou em erro, a área de texto rotulada **Detalhes ou mensagem de erro da sessão selecionada** também será exibida.  
  
 **Exibição**  
 Selecione quais sessões do Snapshot Agent exibir.  
  
 **Status**  
 O status do Snapshot Agent. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Tentando novamente comandos com falha  
  
-   Não está sendo executado  
  
-   Concluído  
  
 **Start Time**  
 A hora de início da sessão.  
  
 **Hora de término**  
 A hora de término da sessão. Se o agente não parou, esse campo estará vazio.  
  
 **Duration**  
 A quantidade de tempo que o Snapshot Agent está em execução nessa sessão. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total da sessão, se a sessão do agente tiver terminado.  
  
 **Mensagem de erro**  
 Se uma sessão terminou em um erro, esse campo exibirá a última mensagem de erro registrada pelo Snapshot Agent. Se uma sessão não terminou em erro, esse campo ficará em branco.  
  
 **Mensagem de Ação**  
 Todas as mensagens informativas e de erro que o Snapshot Agent registrou durante a sessão selecionada.  
  
 **Tempo da Ação**  
 A hora em que a ação descrita na **mensagem de ação** coluna foi executada.  
  
 **Detalhes ou mensagem de erro da sessão selecionada**  
 Será exibida somente se a sessão selecionada exibir um valor de **erro** no **Status** coluna. Essa área de texto exibe informações de erro detalhadas e o comando tentado no momento do erro. Também inclui links para conteúdo adicional relacionado ao erro.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  