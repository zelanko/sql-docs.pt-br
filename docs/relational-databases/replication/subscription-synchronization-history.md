---
description: Assinatura, histórico de sincronização
title: Assinatura, histórico de sincronização | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.synchhistory.f1
- sql13.rep.monitor.subscription.downlevelsynchhistory.f1
ms.assetid: 85f666f6-14ee-4f19-b385-e5cc508aabe4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: db40c8e3848ee5dac3d770e77629555ea87814b3
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88326012"
---
# <a name="subscription-synchronization-history"></a>Assinatura, histórico de sincronização
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  A guia **Histórico de Sincronização** exibe informações detalhadas do Merge Agent, incluindo status, estatísticas de artigo, histórico, mensagens informativas e qualquer mensagem de erro.  
  
## <a name="options"></a>Opções  
 Selecione as sessões do Merge Agent a serem exibidas no menu **Exibir** e, depois, selecione uma sessão específica na grade rotulada **Sessões do Merge Agent**. As informações detalhadas sobre essa sessão são exibidas na grade rotulada **Artigos processados na sessão selecionada**.  
  
 **Exibir**  
 Selecione as sessões do Merge Agent a serem exibidas.  
  
 **Status**  
 A ID do status do Merge Agent no fim da sessão. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Concluído  
  
-   Tentando novamente  
  
-   Executando  
  
 **Start Time**  
 A hora de início da sessão.  
  
 **Hora de término**  
 A hora de término da sessão. Se o agente não parou, esse campo estará vazio.  
  
 **Duration**  
 A quantidade de tempo que o Merge Agent foi executado em uma sessão. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Comandos Carregados**  
 O número de linhas carregado durante a sessão do Merge Agent.  
  
 **Comandos Baixados**  
 O número de linhas baixado durante a sessão do Merge Agent.  
  
 **Mensagem de erro**  
 Se uma sessão tiver terminado em um erro, esse campo exibirá a última mensagem de erro registrada pelo Merge Agent. Se uma sessão não terminou em erro, esse campo ficará em branco.  
  
 **Artigo**  
 O nome de cada artigo na publicação e as fases de processamento posteriores para toda a publicação:  
  
-   **Inicialização**. Refere-se à inicialização do Merge Agent; não é o mesmo que iniciar uma assinatura, que envolve a aplicação de um instantâneo.  
  
-   **Alterações de esquema e inserções em massa**.  
  
-   **Carregar alterações do Publicador**.  
  
-   **Baixar alterações para o Assinante**.  
  
 As fases são incluídas para que a grade possa exibir a quantidade de tempo e a porcentagem do tempo total de cada fase na sessão selecionada.  
  
 **% do total**  
 A porcentagem do tempo de processamento total de cada fase na sessão selecionada.  
  
 **Duration**  
 O tempo gasto em cada fase de processamento. O tempo representa o tempo decorrido, se o Merge Agent estiver sendo executado na sessão no momento, e o tempo total, se o Merge Agent foi executado anteriormente.  
  
 **Insere**  
 O número de linhas inserido nesta fase da sessão selecionada.  
  
 **Atualizações**  
 O número de linhas atualizado nesta fase da sessão selecionada.  
  
 **Deletes**  
 O número de linhas excluído nesta fase da sessão selecionada.  
  
 **Conflitos**  
 O número de conflitos na sessão selecionada.  
  
 **Schema Changes**  
 O número de alterações de esquema na sessão selecionada. As alterações de esquema podem resultar de: alterações sendo replicadas no banco de dados de publicação; adição ou descarte de artigos; e alterações em propriedades de artigo ou publicação.  
  
 **Última mensagem da sessão selecionada**  
 Essa área de texto exibe a última mensagem na sessão selecionada. Se tiver ocorrido um erro, exibirá informações de erro detalhadas e o comando tentado no momento do erro. Também inclui links para conteúdo adicional relacionado ao erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
