---
title: "SQL Server, N&#243; de Mem&#243;ria | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# SQL Server, N&#243; de Mem&#243;ria
  O objeto **Memory Node** do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar o uso de memória de servidor em nós NUMA.  
  
## Contadores de nós de memória  
 Essa tabela descreve os contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** .  
  
|Contadores do Gerenciador de Memória do SQL Server|Descrição|  
|----------------------------------------|-----------------|  
|**Memória do Nó do Banco de Dados (KB)**|Especifica a quantidade de memória que o servidor está usando atualmente nesse nó para páginas de banco de dados.|  
|**Memória do Nó Livre (KB)**|Especifica a quantidade de memória que o servidor não está usando atualmente nesse nó.|  
|**Memória do Nó do Estrangeiro (KB)**|Especifica a quantidade de memória local não NUMA nesse nó.|  
|**Memória do Nó Roubada (KB)**|Especifica a quantidade de memória que o servidor está usando atualmente nesse nó para outras finalidades, sem ser páginas de banco de dados.|  
|**Memória do Nó de Destino**|Especifica a quantidade ideal de memória para esse nó.|  
|**Memória do Nó Total**|Indica a quantidade total de memória que o servidor comprometeu nesse nó.|  
  
## Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto Buffer Manager](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  