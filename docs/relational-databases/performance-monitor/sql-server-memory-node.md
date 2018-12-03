---
title: SQL Server, nó de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: baae3968beb5a007a33627600f5e013f3be848e1
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158664"
---
# <a name="sql-server-memory-node"></a>SQL Server, Nó de Memória
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto **Memory Node** do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar o uso de memória de servidor em nós NUMA.  
  
## <a name="memory-node-counters"></a>Contadores de nós de memória  
 Essa tabela descreve os contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** .  
  
|Contadores do Gerenciador de Memória do SQL Server|Descrição|  
|----------------------------------------|-----------------|  
|**Memória do Nó do Banco de Dados (KB)**|Especifica a quantidade de memória que o servidor está usando atualmente nesse nó para páginas de banco de dados.|  
|**Memória do Nó Livre (KB)**|Especifica a quantidade de memória que o servidor não está usando atualmente nesse nó.|  
|**Memória do Nó do Estrangeiro (KB)**|Especifica a quantidade de memória local não NUMA nesse nó.|  
|**Memória do Nó Roubada (KB)**|Especifica a quantidade de memória que o servidor está usando atualmente nesse nó para outras finalidades, sem ser páginas de banco de dados.|  
|**Memória do Nó de Destino**|Especifica a quantidade ideal de memória para esse nó.|  
|**Memória do Nó Total**|Indica a quantidade total de memória que o servidor comprometeu nesse nó.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto Buffer Manager](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
