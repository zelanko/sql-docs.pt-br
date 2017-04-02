---
title: "Monitorando a replica&#231;&#227;o com o monitor do sistema  | Microsoft Docs"
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
  - "monitorando o desempenho [replicação do SQL Server], Monitor do Sistema"
  - "Monitor do Sistema [SQL Server], replicação"
  - "contadores de desempenho [replicação do SQL Server]"
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Monitorando a replica&#231;&#227;o com o monitor do sistema 
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Monitor de sistema do Windows permite que você use gráficos, gráficos e relatórios para medir a eficiência do seu computador, identificar e solucionar possíveis problemas (como o uso desequilibrado de recursos, hardware insuficiente ou estrutura de programas falhos) e planejar necessidades adicionais de hardware. Para obter mais informações, consulte [monitorar o uso de recursos e 40; Monitor do sistema & 41;](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 O Monitor do Sistema usa objetos e contadores de desempenho que fornecem informações sobre o desempenho de vários processos. É possível medir o desempenho de replicação por meio de contadores associados com os agentes de replicação:  
  
|Agente|Objeto de desempenho|Contador|Descrição|  
|-----------|------------------------|-------------|-----------------|  
|Todos os agentes|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agentes de replicação|Executando|O número de agentes de replicação que estão sendo executados no momento.|  
|Snapshot Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantâneo de replicação|Snapshot: Delivered Cmds/sec|O número de comandos por segundo entregues ao Distribuidor.|  
|Snapshot Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantâneo de replicação|Snapshot: Delivered Trans/sec|O número de transações por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Leitor de log de replicação|Logreader: Delivered Cmds/sec|O número de comandos por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Leitor de log de replicação|Logreader: Delivered Trans/sec|O número de transações por segundo entregues ao Distribuidor.|  
|Agente de Leitor de Log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Leitor de log de replicação|Logreader: Delivery Latency|O período de tempo atual, em milissegundos, passado desde quando as transações foram aplicadas no Publicador até sua entrega no Distribuidor.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Dist. de replicação|Dist: Delivered Cmds/sec|O número de comandos por segundo entregues ao Assinante.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Dist. de replicação|Dist: Delivered Trans/sec|O número de transações por segundo entregues ao Assinante.|  
|Agente de Distribuição|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Dist. de replicação|Dist: Delivery Latency|O período de tempo atual, em milissegundos, passado desde quando as transações foram entregues ao Distribuidor até sua aplicação no Assinante.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem de replicação|Conflitos/s|O número de conflitos por segundo que ocorrem durante o processo de mesclagem.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem de replicação|Alterações baixadas/s|O número de linhas por segundo replicadas do Publicador ao Assinante.|  
|Merge Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mesclagem de replicação|Alterações Carregadas/s |O número de linhas por segundo replicadas do Assinante ao Publicador.|  
  
## Consulte também  
 [Monitoramento e 40; Replicação e 41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  