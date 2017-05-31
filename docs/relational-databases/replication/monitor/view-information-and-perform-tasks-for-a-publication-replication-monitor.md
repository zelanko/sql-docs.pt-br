---
title: "Exibir informações e executar tarefas para uma publicação (Replication Monitor) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d01adb7abcb4c110f826e0cd54814a66c83c0051
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="view-information-and-perform-tasks-for-a-publication-replication-monitor"></a>Exibir informações e executar tarefas para uma publicação (Replication Monitor)
  O Replication Monitor fornece as seguintes guias que incluem informações sobre a publicação selecionada:  
  
-   **Todas as Assinaturas**  
  
     Essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Agentes**  
  
     Essa guia exibe informações sobre todos os agentes usados por uma publicação:  
  
    -   O Agente de Instantâneo, que é usado por todas as publicações.  
  
    -   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
  
    -   O Agente de Leitor de Fila, que é usado pelas publicações transacionais que possuem atualização de assinaturas em fila.  
  
-   **Advertências** (para Distribuidores que executam [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e posterior)  
  
    -   Essa guia permite especificar avisos e alertas para agentes.  
  
-   **Tokens de Rastreamento** (apenas para replicação transacional, para Distribuidores que executam [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e posterior)  
  
     Essa guia permite medir a latência, o período decorrido entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante.  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="to-view-information-and-perform-tasks-for-a-publication"></a>Para exibir informações e executar tarefas para uma publicação  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Para exibir e modificar as propriedades da publicação, clique com o botão direito do mouse na publicação e, em seguida, clique em **Propriedades**.  
  
3.  Para exibir informações sobre assinaturas, clique na guia **Todas as Assinaturas** .  
  
     Para exibir e modificar as propriedades da assinatura, clique com o botão direito do mouse na assinatura  e, então, clique em **Propriedades**. Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. Para obter mais informações, consulte [View Information and Perform Tasks for the Agents Associated With a Subscription &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md) [Exibir informações e executar tarefas para os agentes associados a uma assinatura (Replication Monitor)].  
  
4.  Para exibir informações sobre agentes, clique na guia **Agentes** . Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. Para mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
5.  Para exibir informações sobre advertências de agente e limites, clique na guia **Avisos** . Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
6.  Para exibir informações sobre tokens de rastreamento, clique na guia **Tokens de Rastreamento** . Para obter mais informações sobre como usar tokens de rastreamento, consulte [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
