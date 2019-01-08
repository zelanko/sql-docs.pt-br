---
title: Assinatura, Histórico do Distribuidor para o Assinante (assinatura de instantâneo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.pubtodist.snapshot.f1
ms.assetid: d3575964-f287-4bcf-8d2e-f81a33141b25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a53fb37c9775ef863724db418c574b31ef8a3e2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52784738"
---
# <a name="subscription-distributor-to-subscriber-history-snapshot-subscription"></a>Assinatura, Histórico do Distribuidor para o Assinante (assinatura de instantâneo)
  A guia **Histórico do Distribuidor para o Assinante** exibe informações detalhadas sobre o Distribution Agent, incluindo status, histórico, mensagens informativas e qualquer mensagem de erro.  
  
## <a name="options"></a>Opções  
 Selecione as sessões do Distribution Agent a serem exibidas no menu **Exibir** e depois selecione uma sessão específica na grade rotulada **Sessões do Distribution Agent**. Informações detalhadas sobre essa sessão são exibidas na grade rotulada **Ações na sessão selecionada**. Se a sessão selecionada terminou em erro, a área de texto rotulada **Detalhes ou mensagem de erro da sessão selecionada** também será exibida.  
  
 **Exibir**  
 Selecione as sessões do Distribution Agent a serem exibidas.  
  
 **Status**  
 O status do Distribution Agent. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Concluído  
  
-   Tentando novamente  
  
-   Executando  
  
 **Start Time**  
 A hora de início da sessão.  
  
 **Hora de término**  
 A hora de término da sessão. Se o agente não parou, esse campo estará vazio.  
  
 **Duration**  
 A quantidade de tempo que o Distribution Agent está em execução nessa sessão. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total da sessão, se a sessão do agente tiver terminado.  
  
 **Mensagem de erro**  
 Se uma sessão terminou em um erro, esse campo exibirá a última mensagem de erro registrada pelo Distribution Agent. Se uma sessão não terminou em erro, esse campo ficará em branco.  
  
 **Mensagem de Ação**  
 Todas as mensagens informativas e de erro que o Distribution Agent registrou durante a sessão selecionada.  
  
 **Tempo da Ação**  
 O tempo no qual a ação descrita na coluna **Mensagem de Ação** foi executada.  
  
 **Detalhes ou mensagem de erro da sessão selecionada**  
 Exibido somente se a sessão selecionada exibir um valor de **Erro** na coluna **Status** . Essa área de texto exibe informações de erro detalhadas e o comando tentado no momento do erro. Também inclui links para conteúdo adicional relacionado ao erro.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Exibir informações e realizar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [Monitorando a Replicação](monitoring-replication.md)   
 [Visão geral dos agentes de replicação](agents/replication-agents-overview.md)  
  
  
