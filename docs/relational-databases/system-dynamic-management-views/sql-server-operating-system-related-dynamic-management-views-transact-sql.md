---
title: Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operating systems [SQL Server], dynamic management objects
- SQL Operating System dynamic management objects [SQL Server]
- SQL OS dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], SQL OS
ms.assetid: 3030c86a-0a74-4fed-ac0f-392e244cb965
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac714a00dcc4b5a858d12ca0789a44e4c9ebb30e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702778"
---
# <a name="sql-server-operating-system-related-dynamic-management-views-transact-sql"></a>Exibições de gerenciamento dinâmico relacionadas ao sistema operacional do SQL Server (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta seção contém as exibições de gerenciamento dinâmico associados ao Sistema Operacional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOS). O SQLOS é responsável por gerenciar os recursos do sistema operacional específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||  
|-|-|  
|[sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)|[sys.dm_os_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-pools-transact-sql.md)|  
|[sys.dm_os_child_instances &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-child-instances-transact-sql.md)|[sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)|  
|[sys.dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)|[sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)|  
|[sys.dm_os_dispatcher_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|[sys.dm_os_process_memory &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md)|  
|[DM os_host_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)|[sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)|  
|[sys.dm_os_hosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)|[sys.dm_os_stacks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-stacks-transact-sql.md)|  
|[sys.DM-sistema operacional-objeto de trabalho &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-job-object-transact-sql.md)||
|[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)|[sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)|  
|[sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md)|[sys.dm_os_sys_memory &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-memory-transact-sql.md)|  
|[sys.dm_os_memory_brokers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-brokers-transact-sql.md)|[sys.dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)|  
|[sys.dm_os_memory_cache_clock_hands &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-clock-hands-transact-sql.md)|[sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)|  
|[sys.dm_os_memory_cache_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)|[sys.dm_os_virtual_address_dump &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-virtual-address-dump-transact-sql.md)|  
|[sys.dm_os_memory_cache_entries &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)|[sys.dm_os_volume_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-volume-stats-transact-sql.md)|  
|[sys.dm_os_memory_cache_hash_tables &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-hash-tables-transact-sql.md)|[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|[sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)|[sys.dm_os_waiting_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md)|  
|[sys.dm_os_memory_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)|[sys.dm_os_windows_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)|  
|[sys.dm_os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)|[sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)|  
  
 As exibições de gerenciamento dinâmico relacionadas ao Sistema Operacional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].  
  
|||  
|-|-|  
|**sys.dm_os_function_symbolic_name**|**sys.dm_os_ring_buffers**|  
|**sys.dm_os_memory_allocations**|**sys.dm_os_sublatches**|  
|**sys.dm_os_worker_local_storage**||  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

