---
title: Monitorando a replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 81f596d2-27a5-489d-bf8d-0f4361decd02
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c18872dee35e55da6af067f9459e15f99f9402bd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165436"
---
# <a name="monitoring-replication"></a>Replicação de monitoramento
  O Replication Monitor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é uma ferramenta gráfica que permite monitorar a integridade geral de uma topologia de replicação. O Replication Monitor fornece informações detalhadas sobre o status e o desempenho das publicações e das assinaturas, permitindo responder a perguntas comuns tais como:  
  
-   Meu sistema de replicação está íntegro?  
  
-   Quais assinaturas estão lentas?  
  
-   A minha assinatura transacional está muito atrás na fila?  
  
-   Quanto tempo uma transação confirmada agora, levará para alcançar um Assinante em replicação transacional?  
  
-   Por que minha assinatura de mesclagem está lenta?  
  
-   Por que um agente não está executando?  
  
 Para monitorar a replicação o usuário deve ser membro da função de servidor fixa **sysadmin** no Distribuidor ou membro da função de banco de dados fixa **replmonitor** no banco de dados de distribuição. Um administrador de sistema pode adicionar qualquer usuário à função **replmonitor** , o que permite que o usuário exiba a atividade de replicação no Replication Monitor. No entanto, o usuário não pode administrar a replicação.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir fornecem mais informações sobre os recursos do Replication Monitor.  
  
 [Visão geral da interface do Replication Monitor](overview-of-the-replication-monitor-interface.md)  
 Descreve cada janela e guia no Replication Monitor e fornece informações sobre como responder às perguntas listadas anteriormente.  
  
 [Iniciar o Replication Monitor](start-the-replication-monitor.md)  
 Descreve como iniciar o Replication Monitor.  
  
 [Permitir que não administradores usem o Replication Monitor](allow-non-administrators-to-use-replication-monitor.md)  
 Descreve como atribuir permissões a não administradores de forma que eles possam usar o Replication Monitor.  
  
 [Adicionar e remover publicadores do Replication Monitor](add-and-remove-publishers-from-replication-monitor.md)  
 Descreve como adicionar ou remover Publicadores do Replication Monitor.  
  
 [Atualizar dados no Replication Monitor](refresh-data-in-replication-monitor.md)  
 Descreve como atualizar dados no Replication Monitor.  
  
 [Monitorar o desempenho com o Replication Monitor](monitor-performance-with-replication-monitor.md)  
 Descreve como monitorar o desempenho no Replication Monitor, inclusive as informações em como definir limiares de desempenho. Inclui informações sobre as estatísticas em nível de artigo para a replicação de mesclagem, as quais fornecem uma visão detalhada do processamento.  
  
 [Medir a latência e validar as conexões para a replicação transacional](measure-latency-and-validate-connections-for-transactional-replication.md)  
 Descreve os tokens de rastreamento que permitem medir o desempenho de uma topologia de replicação transacional.  
  
 [Monitorar agentes de replicação](../agents/replication-agents.md)  
 Descreve como localizar informações sobre cada agente de replicação.  
  
 [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md)  
 Descreve os avisos, limiares e alertas que você pode definir no Replication Monitor. Recomendamos habilitar os avisos para a sua topologia, para que esteja informado sobre o status e o desempenho de maneira oportuna.  
  
 [Desempenho de Cache, da atualização e do Replication Monitor](caching-refresh-and-replication-monitor-performance.md)  
 Descreve como o Replication Monitor armazena os dados em cache para melhorar o desempenho; explica como a atualização da interface de usuário se relaciona à atualização do cache.  
  
 [Exibir o status da publicação e da assinatura no Replication Monitor](view-publication-and-subscription-status-in-replication-monitor.md)  
 Descreve como exibir informações de status em uma Publicação ou Assinatura usando o Replication Monitor.  
  
 [Exibir informações e executar tarefas para um Publicador &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
 Descreve como exibir informações e executar tarefas para um Publicador usando o Replication Monitor.  
  
 [Exibir informações e executar tarefas para uma publicação &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)  
 Descreve como exibir informações e executar tarefas para uma publicação usando o Replication Monitor.  
  
 [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-publication-agents.md)  
 Descreve como exibir informações e executar tarefas para os agentes associados com uma publicação usando o Replication Monitor.  
  
 [Exibir informações e realizar tarefas para uma assinatura &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
 Descreve como exibir informações e executar tarefas para uma assinatura usando o Replication Monitor.  
  
 [Exibir informações e realizar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-subscription-agents.md)  
 Descreve como exibir informações e executar tarefas para os agentes associados com uma assinatura usando o Replication Monitor.  
  
  
