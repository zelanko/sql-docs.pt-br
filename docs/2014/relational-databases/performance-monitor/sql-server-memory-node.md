---
title: SQL Server, nó de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 32a2296fdb68e640ce8ebfc8dd9cdb351666b337
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250574"
---
# <a name="sql-server-memory-node"></a>SQL Server, Nó de Memória
  O objeto de **nó** de memória [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Microsoft fornece contadores para monitorar o uso de memória do servidor em nós numa.  
  
## <a name="memory-node-counters"></a>Contadores de nós de memória  
 Essa tabela descreve os contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** .  
  
|Contadores do Gerenciador de Memória do SQL Server|DESCRIÇÃO|  
|----------------------------------------|-----------------|  
|**Memória do nó do banco de dados (KB)**|Especifica a quantidade de memória que o servidor está usando atualmente nesse nó para páginas de banco de dados.|  
|**Memória de nó livre (KB)**|Especifica a quantidade de memória que o servidor não está usando atualmente nesse nó.|  
|**Memória do nó estrangeiro (KB)**|Especifica a quantidade de memória local não NUMA nesse nó.|  
|**Nó de memória roubada (KB)**|Especifica a quantidade de memória que o servidor está usando atualmente nesse nó para outras finalidades, sem ser páginas de banco de dados.|  
|**Memória do nó de destino**|Especifica a quantidade ideal de memória para esse nó.|  
|**Memória total do nó**|Indica a quantidade total de memória que o servidor comprometeu nesse nó.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto Gerenciador de buffer](sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
