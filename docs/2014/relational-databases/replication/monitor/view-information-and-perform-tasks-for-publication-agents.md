---
title: Exibir informações e executar tarefas para os agentes associados a uma publicação (Replication Monitor) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a92f56a6a9c68d984323ba8801755f87a1eaaec7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758028"
---
# <a name="view-information-and-perform-tasks-for-the-agents-associated-with-a-publication-replication-monitor"></a>Exibir informações e executar tarefas para os agentes associados a uma publicação (Replication Monitor)
  O Replication Monitor fornece a guia **Agentes** , que inclui informações sobre os agentes associados com a publicação selecionada. Para Agente de Distribuição e Agente de Mesclagem, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-subscription-agents.md).  
  
 Essa guia exibe informações sobre os seguintes agentes:  
  
-   O Agente de Instantâneo, que é usado por todas as publicações.  
  
-   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
  
-   O Agente de Leitor de Fila, que é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
 Para exibir mais informações sobre as opções nessa guia, clique em **Ajuda** na barra de menu. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>Para exibir informações e executar tarefas para os agentes associados com uma publicação  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Para exibir informações sobre agentes, clique na guia **Agentes** . Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente (como mensagens informativas e qualquer mensagem de erro), clique com o botão direito do mouse no agente e então clique em **Exibir Detalhes**.  
  
    -   Para exibir informações detalhadas sobre o trabalho que executa o agente (como o cronograma, detalhes da etapa de trabalho e outras), clique com o botão direito do mouse no agente e então clique em **Propriedades**.  
  
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../agents/replication-agent-profiles.md).  
  
    -   Para iniciar um agente que não está sendo executado, clique com o botão direito do mouse no agente e então clique em **Iniciar Agente**.  
  
    -   Para interromper um agente que está sendo executado, clique com o botão direito do mouse no agente e então clique em **Interromper Agente**.  
  
## <a name="see-also"></a>Consulte também  
 [Definir limites e avisos no Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md)   
 [Exibir informações e executar tarefas para uma publicação &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Administração do agente de replicação](../agents/replication-agent-administration.md)   
 [Monitorando a Replicação](../monitoring-replication.md)  
  
  
