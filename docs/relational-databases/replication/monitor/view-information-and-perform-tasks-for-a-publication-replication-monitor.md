---
title: "Exibir informa&#231;&#245;es e executar tarefas para uma publica&#231;&#227;o (Replication Monitor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exibindo informações de publicação"
  - "publicações [replicação do SQL Server], exibindo informações"
  - "publicações [replicação do SQL Server], tarefas do Replication Monitor"
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Exibir informa&#231;&#245;es e executar tarefas para uma publica&#231;&#227;o (Replication Monitor)
  O Replication Monitor fornece as seguintes guias que incluem informações sobre a publicação selecionada:  
  
-   **Todas as Assinaturas**  
  
     Essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Agentes**  
  
     Essa guia exibe informações sobre todos os agentes usados por uma publicação:  
  
    -   O Agente de Instantâneo, que é usado por todas as publicações.  
  
    -   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
  
    -   O Agente de Leitor de Fila, que é usado pelas publicações transacionais que possuem atualização de assinaturas em fila.  
  
-   **Avisos** (para distribuidores executando [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e posterior)  
  
    -   Essa guia permite especificar avisos e alertas para agentes.  
  
-   **Os Tokens de rastreamento** (replicação transacional somente para distribuidores executando [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e posterior)  
  
     Essa guia permite medir a latência, o período decorrido entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante.  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para exibir informações e executar tarefas para uma publicação  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Para exibir e modificar propriedades de publicação, com o botão direito na publicação e, em seguida, clique em **propriedades**.  
  
3.  Para exibir informações sobre assinaturas, clique na guia **Todas as Assinaturas** .  
  
     Para exibir e modificar propriedades de assinatura, clique com botão direito a assinatura e, em seguida, clique em **propriedades**. Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
4.  Para exibir informações sobre agentes, clique o **agentes** guia. Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
5.  Para exibir informações sobre limites e avisos de agente, clique o **avisos** guia. Para obter mais informações, consulte [definir limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
6.  Para exibir informações sobre tokens de rastreamento, clique o **Tokens de rastreamento** guia. Para obter mais informações sobre como usar os tokens de rastreamento, consulte [medidas latência e validar conexões para replicação transacional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## Consulte também  
 [Visualizar e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  