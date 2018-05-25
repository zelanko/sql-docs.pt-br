---
title: sys.dm_exec_query_parallel_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
caps.latest.revision: 1
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f2bc4634a5e2fddb4a3c8eda009eb28019089596
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Retorna a informações de disponibilidade do trabalho por nó.  
  
|Nome|Tipo de dados|Description|  
|----------|---------------|-----------------|  
|**node_id**|**Int**|ID do nó NUMA.|  
|**scheduler_count**|**Int**|Número de agendadores neste nó.|  
|**max_worker_count**|**Int**|Número máximo de trabalhadores para consultas paralelas.|  
|**reserved_worker_count**|**Int**|Número de trabalhadores reservados por consultas paralelas, mais o número de trabalhadores principais usados por todas as solicitações.| 
|**free_worker_count**|**Int**|Número de trabalhadores disponíveis para as tarefas.<br /><br />**Observação:** cada solicitação de entrada consome trabalho pelo menos 1, que é subtraído de contagem de trabalho livres.  É possível que a contagem de trabalho livres pode ser um número negativo em um servidor muito carregado.| 
|**used_worker_count**|**Int**|Número de trabalhadores usados por consultas paralelas.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   
 
## <a name="examples"></a>Exemplos  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. Exibindo a disponibilidade de trabalho paralelas atual  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
