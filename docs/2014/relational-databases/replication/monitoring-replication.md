---
title: Monitorando a replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 615582b2d961f87a2d3df151175d7bd5d06e305f
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000379"
---
# <a name="monitoring-replication"></a>Monitorando (Replicação)
  Monitorar uma topologia de replicação é um aspecto importante na implantação da replicação. Já que a atividade de replicação é distribuída, é essencial controlar sua atividade e o status em todos os computadores envolvidos na replicação. As seguintes ferramentas podem ser usadas para monitorar a replicação:  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)][!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]Replication Monitor  
  
     O Replication Monitor é a ferramenta mais importante para monitorar a replicação, apresentando uma exibição do Publicador dedicada a toda atividade de replicação. Para obter mais informações, consulte [monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md).  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssManStudioFull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] fornece o acesso ao Replication Monitor. Também permite exibir o status atual e a última mensagem registrada pelos seguintes agentes e permite iniciar e parar cada agente: Agent de Leitor de Log, Agente de Instantâneo, Agente de Mesclagem e Agente de Distribuição. Para obter mais informações, consulte [Monitor Replication Agents](monitor/monitor-replication-agents.md).  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] e RMO (Replication Management Objects)  
  
     Ambas as interfaces permitem monitorar todos os tipos de replicação do Distribuidor. A replicação de mesclagem fornece também a capacidade de monitorar a replicação a partir do Assinante.  
  
-   Alertas para eventos do agente de replicação  
  
     A replicação fornece vários alertas predefinidos para os eventos do agente de replicação e você pode criar alertas adicionais, se necessário. Os alertas podem ser usados para acionar uma resposta automatizada a um evento e/ou notificar um administrador. Para obter mais informações, consulte [Usar alertas para eventos do agente de replicação](agents/use-alerts-for-replication-agent-events.md).  
  
-   Monitor do Sistema  
  
     O Monitor do Sistema pode ser útil para monitorar o desempenho, ao fornecer vários contadores para a replicação. Para obter mais informações, consulte [Monitoring Replication with System Monitor](monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Perguntas frequentes sobre administração de replicação](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Práticas recomendadas para a administração de replicação](administration/best-practices-for-replication-administration.md)   

  
  
