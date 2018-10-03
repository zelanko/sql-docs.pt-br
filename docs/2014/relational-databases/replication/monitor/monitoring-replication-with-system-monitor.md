---
title: Monitorando a replicação com o Monitor do Sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7ebe259824ab5c5efb2d85cda72e32bc15df429d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072176"
---
# <a name="monitoring-replication-with-system-monitor"></a>Monitorando a replicação com o monitor do sistema
  O Monitor do Sistema do Windows[!INCLUDE[msCoName](../../../includes/msconame-md.md)] permite o uso de gráficos e relatórios para medir a eficiência do seu computador, e a identificação e solução de possíveis problemas (como uso desbalanceado de recursos, hardware insuficiente ou design de programa inadequado), e o planejamento de requisitos adicionais de hardware. Para obter mais informações, veja [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 O Monitor do Sistema usa objetos e contadores de desempenho que fornecem informações sobre o desempenho de vários processos. É possível medir o desempenho de replicação por meio de contadores associados com os agentes de replicação:  
  
|Agente|Objeto de desempenho|Contador|Description|  
|-----------|------------------------|-------------|-----------------|  
|Todos os agentes|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agentes de replicação|Executando|O número de agentes de replicação que estão sendo executados no momento.|  
|Snapshot Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantâneo de Replicação|Snapshot: Delivered Cmds/sec|O número de comandos por segundo entregues ao Distribuidor.|  
|Snapshot Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantâneo de Replicação|Snapshot: Delivered Trans/sec|O número de transações por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Logreader: Delivered Cmds/sec|O número de comandos por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Logreader: Delivered Trans/sec|O número de transações por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Logreader: Delivery Latency|O período de tempo atual, em milissegundos, passado desde quando as transações foram aplicadas no Publicador até sua entrega no Distribuidor.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist: Delivered Cmds/sec|O número de comandos por segundo entregues ao Assinante.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist: Delivered Trans/sec|O número de transações por segundo entregues ao Assinante.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist: Delivery Latency|O período de tempo atual, em milissegundos, passado desde quando as transações foram entregues ao Distribuidor até sua aplicação no Assinante.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem de Replicação|Conflitos/s|O número de conflitos por segundo que ocorrem durante o processo de mesclagem.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem de Replicação|Alterações baixadas/s|O número de linhas por segundo replicadas do Publicador ao Assinante.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem de Replicação|Alterações Carregadas/s|O número de linhas por segundo replicadas do Assinante ao Publicador.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitoramento &#40;replicação&#41;](../monitoring-replication.md)  
  
  
