---
title: "Monitoramento (replicação) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0470bd4cb87593b41b41251a0e8f48f94a55556e
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="monitoring-replication"></a>Monitorando (Replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitorar uma topologia de replicação é um aspecto importante na implantação da replicação. Já que a atividade de replicação é distribuída, é essencial controlar sua atividade e o status em todos os computadores envolvidos na replicação. As seguintes ferramentas podem ser usadas para monitorar a replicação:  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor  
  
     O Replication Monitor é a ferramenta mais importante para monitorar a replicação, apresentando uma exibição do Publicador dedicada a toda atividade de replicação. Para obter mais informações, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] fornece o acesso ao Replication Monitor. Também permite exibir o status atual e a última mensagem registrada pelos seguintes agentes e permite iniciar e parar cada agente: Agent de Leitor de Log, Agente de Instantâneo, Agente de Mesclagem e Agente de Distribuição. Para obter mais informações, consulte [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] e RMO (Replication Management Objects)  
  
     Ambas as interfaces permitem monitorar todos os tipos de replicação do Distribuidor. A replicação de mesclagem fornece também a capacidade de monitorar a replicação a partir do Assinante.  
  
-   Alertas para eventos do agente de replicação  
  
     A replicação fornece vários alertas predefinidos para os eventos do agente de replicação e você pode criar alertas adicionais, se necessário. Os alertas podem ser usados para acionar uma resposta automatizada a um evento e/ou notificar um administrador. Para obter mais informações, consulte [Usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
-   Monitor do Sistema  
  
     O Monitor do Sistema pode ser útil para monitorar o desempenho, ao fornecer vários contadores para a replicação. Para obter mais informações, consulte [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Administração &#40;Replicação&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
