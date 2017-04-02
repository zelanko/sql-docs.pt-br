---
title: "Monitorando (Replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "monitorando o desempenho [replicação do SQL Server], sobre o monitoramento de replicação"
  - "replicação transacional, monitorando"
  - "monitorando [replicação do SQL Server]"
  - "monitorando a replicação de mesclagem [replicação do SQL Server]"
  - "replicação de instantâneo [SQL Server], monitorando"
  - "replicação [SQL Server], monitorando"
  - "administrando a replicação, monitorando"
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Monitorando (Replica&#231;&#227;o)
  Monitorar uma topologia de replicação é um aspecto importante na implantação da replicação. Já que a atividade de replicação é distribuída, é essencial controlar sua atividade e o status em todos os computadores envolvidos na replicação. As seguintes ferramentas podem ser usadas para monitorar a replicação:  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor  
  
     O Replication Monitor é a ferramenta mais importante para monitorar a replicação, apresentando uma exibição do Publicador dedicada a toda atividade de replicação. Para obter mais informações, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] fornece acesso ao Replication Monitor. Também permite exibir o status atual e a última mensagem registrada pelos seguintes agentes e permite iniciar e parar cada agente: Agent de Leitor de Log, Agente de Instantâneo, Agente de Mesclagem e Agente de Distribuição. Para obter mais informações, consulte [monitorar agentes de replicação](../../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] e Replication Management Objects (RMO)  
  
     Ambas as interfaces permitem monitorar todos os tipos de replicação do Distribuidor. A replicação de mesclagem fornece também a capacidade de monitorar a replicação a partir do Assinante.  
  
-   Alertas para eventos do agente de replicação  
  
     A replicação fornece vários alertas predefinidos para os eventos do agente de replicação e você pode criar alertas adicionais, se necessário. Os alertas podem ser usados para acionar uma resposta automatizada a um evento e/ou notificar um administrador. Para obter mais informações, consulte [usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
-   Monitor do Sistema  
  
     O Monitor do Sistema pode ser útil para monitorar o desempenho, ao fornecer vários contadores para a replicação. Para obter mais informações, consulte [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  
## Consulte também  
 [Administração e 40; Replicação e 41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Práticas recomendadas para administração de replicação](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  