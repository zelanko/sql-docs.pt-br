---
title: "Assinatura, Hist&#243;rico de Sincroniza&#231;&#227;o (assinatura de mesclagem, SQL Server 2000) | Microsoft Docs"
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
  - "sql13.rep.monitor.subscription.downlevelsynchhistory.f1"
ms.assetid: 0a0deab2-1c08-4371-9681-d9403e0236cc
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Assinatura, Hist&#243;rico de Sincroniza&#231;&#227;o (assinatura de mesclagem, SQL Server 2000)
  O **histórico de sincronização** guia exibe informações detalhadas sobre o Merge Agent, incluindo status, histórico, mensagens informativas e qualquer mensagem de erro.  
  
## Opções  
 Selecione as sessões do Merge Agent a serem exibidas no menu **Exibir** e, depois, selecione uma sessão específica na grade rotulada **Sessões do Merge Agent**. Informações detalhadas sobre essa sessão são exibidas na grade rotulada **Ações na sessão selecionada**. Se a sessão selecionada terminou em erro, a área de texto rotulada **Detalhes ou mensagem de erro da sessão selecionada** também será exibida.  
  
 **Exibição**  
 Selecione as sessões do Merge Agent a serem exibidas. Normalmente, o Merge Agent é executado continuamente, portanto, pode haver somente uma sessão para exibição.  
  
 **Status**  
 O status do Merge Agent. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Concluído  
  
-   Tentando novamente  
  
-   Executando  
  
 **Start Time**  
 A hora de início da sessão.  
  
 **Hora de término**  
 A hora de término da sessão. Se o agente não parou, esse campo estará vazio.  
  
 **Duration**  
 O tempo que o Merge Agent está em execução nessa sessão. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total da sessão, se a sessão do agente tiver terminado.  
  
 **Mensagem de erro**  
 Se uma sessão tiver terminado em um erro, esse campo exibirá a última mensagem de erro registrada pelo Merge Agent. Se uma sessão não terminou em erro, esse campo ficará em branco.  
  
 **Mensagem de Ação**  
 Todas as mensagens informativas e de erro que o Merge Agent registrou durante a sessão selecionada.  
  
 **Tempo da Ação**  
 A hora em que a ação descrita na **mensagem de ação** coluna foi executada.  
  
 **Detalhes ou mensagem de erro da sessão selecionada**  
 Exibido somente se a sessão selecionada exibir um valor de **erro** no **Status** coluna. Essa área de texto exibe informações de erro detalhadas e o comando tentado no momento do erro. Também inclui links para conteúdo adicional relacionado ao erro.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  