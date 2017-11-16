---
title: "Informações sobre o distribuidor, Agentes | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.Distributor.commonjobs..f1
ms.assetid: 5d601a64-6af0-42f9-81b1-cf0087f1c50d
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 732843c1a3d3e659b08ab5e88bca333aa7e804d8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="distributor-information-agents"></a>Distributor Information, Agentes
  A guia **Agentes** exibe informações sobre os agentes e trabalhos de manutenção associados com o Publicador e o Assinante.  
  
 Os agentes disponíveis na guia **Agentes** de uma exibição Distribuidor no Distribuidor incluem todos os agentes disponíveis na guia **Agentes** de um Publicador. No entanto, a guia **Agentes** de uma exibição Distribuidor no Distribuidor também inclui um Agente Distribuidor e um Merge Agent.  
  
 Para obter mais informações sobre os agentes Snapshot, Log Reader e Queue Reader, e os trabalhos de manutenção, consulte [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md). Observe que, quando você exibe informações de agente na guia **Agentes** de um Distribuidor, as informações do Publicador estão presentes para os agentes Snapshot e Log Reader. No entanto, na guia **Agentes** de uma exibição Distribuidor no Distribuidor, ainda é possível selecionar **Agente Distribuidor** e **Merge Agent**.  
  
## <a name="options"></a>Opções  
 As seções a seguir descrevem os dados exibidos nesta guia do Agente Distribuidor e do Merge Agent.  
  
### <a name="distributor-agent"></a>Agente Distribuidor  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Repetir  
  
-   Executando  
  
-   Não está em execução  
  
-   Nunca iniciado  
  
 **Publicador**  
 A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador.  
  
 **Publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Assinatura**  
 O nome da assinatura, no formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicação: push, pull ou Anônima.  
  
 **Última Hora de Início**  
 A última hora de início do agente.  
  
 **Duration**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual os comandos de inicialização são confirmados no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **Latência**  
 É o tempo, em segundos, que decorreu entre a alteração mais recente sendo confirmada no banco de dados de publicação e o comando correspondente sendo confirmado no banco de dados de distribuição.  
  
 **#Trans**  
 O número de transações confirmado no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **#Cmds**  
 O número de comandos confirmado no banco de dados de distribuição durante a execução mais recente do agente. Um comando é igual a uma alteração de dados, como uma atualização.  
  
 **Avg. #Cmds**  
 O número médio de comandos por transação durante a execução mais recente do agente.  
  
### <a name="merge-agent"></a>Merge Agent  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Repetir  
  
-   Executando  
  
-   Não está em execução  
  
-   Nunca iniciado  
  
 **Publicador**  
 A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador.  
  
 **Publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Assinatura**  
 O nome da assinatura, no formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicação: push, pull ou Anônima.  
  
 **Última Hora de Início**  
 A última hora de início do agente.  
  
 **Duration**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual as alterações são confirmadas no banco de dados de distribuição.  
  
 **Inserções do Publicador**  
 Número de comandos INSERT aplicados no Publicador.  
  
 **Atualizações do Publicador**  
 Número de comandos UPDATE aplicados no Publicador.  
  
 **Exclusões do Publicador**  
 Número de comandos DELETE aplicados no Publicador.  
  
 **Conflitos do Publicador**  
 O número de conflitos por segundo que ocorrem no Publicador durante o processo de mesclagem.  
  
 **Inserções do Assinante**  
 Número de comandos INSERT aplicados no Assinante.  
  
 **Atualizações do Assinante**  
 Número de comandos UPDATE aplicados no Assinante.  
  
 **Exclusões do Assinante**  
 Número de comandos DELETE aplicados no Assinante.  
  
 **Conflitos do Assinante**  
 O número de conflitos por segundo que ocorrem no Assinante durante o processo de mesclagem.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para um Publicador &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
