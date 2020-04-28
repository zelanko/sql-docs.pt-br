---
title: sys. dm_exec_query_parallel_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 000dd995427f8eafec759688db1ab76a6546b789
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68263264"
---
# <a name="sysdm_exec_query_parallel_workers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Retorna informações de disponibilidade de trabalhador por nó.  
  
|Nome|Tipo de dados|Descrição|  
|----------|---------------|-----------------|  
|**node_id**|**int**|ID do nó NUMA.|  
|**scheduler_count**|**int**|Número de agendadores neste nó.|  
|**max_worker_count**|**int**|Número máximo de trabalhadores para consultas paralelas.|  
|**reserved_worker_count**|**int**|Número de trabalhadores reservados por consultas paralelas, mais o número de trabalhos principais usados por todas as solicitações.| 
|**free_worker_count**|**int**|Número de trabalhadores disponíveis para tarefas.<br /><br />**Observação:** cada solicitação de entrada consome pelo menos um trabalho, que é subtraído da contagem de trabalhadores livres.  É possível que a contagem de trabalhadores gratuitas possa ser um número negativo em um servidor muito carregado.| 
|**used_worker_count**|**int**|Número de trabalhadores usados por consultas paralelas.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
 
## <a name="examples"></a>Exemplos  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>a. Exibindo a disponibilidade atual do operador Parallel  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys. dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
