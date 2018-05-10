---
title: sys.DM os_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_workers_TSQL
- sys.dm_os_workers_TSQL
- dm_os_workers
- sys.dm_os_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_workers dynamic management view
ms.assetid: 4d5d1e52-a574-4bdd-87ae-b932527235e8
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fb4ea904413d32b2f11979130bce42bb7730255d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmosworkers-transact-sql"></a>sys.dm_os_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada trabalhador no sistema.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_workers**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|worker_address|**varbinary(8)**|Endereço de memória do trabalhador.|  
|status|**Int**|Somente para uso interno.|  
|is_preemptive|**bit**|1 = o trabalhador está executando com agendamento preventivo. Qualquer trabalhador que esteja executando código externo será executado sob agendamento preemptivo.|  
|is_fiber|**bit**|1 = o trabalhador está executando com lightweight pooling. Para obter mais informações, consulte [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).|  
|is_sick|**bit**|1 = o trabalhador está preso tentando obter um bloqueio de giro. Se este bit estiver definido, isto pode indicar um problema com contenção em um objeto frequentemente acessado.|  
|is_in_cc_exception|**bit**|1 = atualmente o trabalhador está tratando uma exceção não relativa ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_fatal_exception|**bit**|Especifica se este trabalhador recebeu uma exceção fatal.|  
|is_inside_catch|**bit**|1 = atualmente o trabalhador está tratando uma exceção.|  
|is_in_polling_io_completion_routine|**bit**|1 = atualmente o trabalhador está executando uma rotina de conclusão de E/S para uma E/S pendente. Para obter mais informações, consulte [sys.DM io_pending_io_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-pending-io-requests-transact-sql.md).|  
|context_switch_count|**Int**|Número de alternâncias de contexto do agendador executadas por este trabalhador.|  
|pending_io_count|**Int**|Número de E/Ss físicas executadas por este trabalhador.|  
|pending_io_byte_count|**bigint**|Número total de bytes para todas as E/Ss físicas pendentes para este trabalhador.|  
|pending_io_byte_average|**Int**|Número médio de bytes das E/Ss físicas para este trabalhador.|  
|wait_started_ms_ticks|**bigint**|Ponto no tempo, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando este trabalhador entrou no estado suspenso. Subtrair este valor de ms_ticks em [sys.DM os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) retorna o número de milissegundos que o trabalho está aguardando.|  
|wait_resumed_ms_ticks|**bigint**|Ponto no tempo, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando este trabalhador entrou no estado RUNNABLE. Subtrair este valor de ms_ticks em [sys.DM os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) retorna o número de milissegundos que o funcionário esteve na fila executável.|  
|task_bound_ms_ticks|**bigint**|Ponto no tempo, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando uma tarefa está associada a este trabalhador.|  
|worker_created_ms_ticks|**bigint**|Ponto no tempo, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando um trabalho é criado.|  
|exception_num|**Int**|Número do erro da última exceção que este trabalhador encontrou.|  
|exception_severity|**Int**|Gravidade da última exceção que este trabalhador encontrou.|  
|exception_address|**varbinary(8)**|Endereço de código que lançou a exceção|  
|affinity|**bigint**|A afinidade do thread do trabalhador. Corresponde a afinidade do thread no [os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md).|  
|state|**nvarchar(60)**|Estado do trabalhador. Pode ser um dos seguintes valores:<br /><br /> INIT = atualmente o trabalhador está sendo inicializado.<br /><br /> RUNNING = atualmente o trabalhador está executando de modo não preemptivo ou preemptivo.<br /><br /> RUNNABLE = o trabalhador está pronto para execução no agendador.<br /><br /> SUSPENDED = o trabalhador está atualmente suspenso, aguardando que um evento envie um sinal para ele.|  
|start_quantum|**bigint**|Tempo, em milissegundos, no início da execução atual deste trabalhador.|  
|end_quantum|**bigint**|Tempo, em milissegundos, no final da execução atual deste trabalhador.|  
|last_wait_type|**nvarchar(60)**|Tipo da última espera. Para obter uma lista de tipos de espera, consulte [sys.DM os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|return_code|**Int**|Valor de retorno da última espera. Pode ser um dos seguintes valores:<br /><br /> 0 =SUCCESS<br /><br /> 3 = DEADLOCK<br /><br /> 4 = PREMATURE_WAKEUP<br /><br /> 258 = TIMEOUT|  
|quantum_used|**bigint**|Somente para uso interno.|  
|max_quantum|**bigint**|Somente para uso interno.|  
|boost_count|**Int**|Somente para uso interno.|  
|tasks_processed_count|**Int**|Número de tarefas que este trabalhador processou.|  
|fiber_address|**varbinary(8)**|Endereço de memória da fibra à qual este trabalhador está associado.<br /><br /> NULL = o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está configurado para lightweight pooling.|  
|task_address|**varbinary(8)**|Endereço de memória da tarefa atual. Para obter mais informações, consulte [os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).|  
|memory_object_address|**varbinary(8)**|Endereço de memória do objeto de memória do trabalhador. Para obter mais informações, consulte [sys.DM os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).|  
|thread_address|**varbinary(8)**|Endereço de memória do thread associado a este trabalhador. Para obter mais informações, consulte [os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md).|  
|signal_worker_address|**varbinary(8)**|Endereço de memória do trabalhador que sinalizou este objeto pela última vez. Para obter mais informações, consulte [sys.DM os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|scheduler_address|**varbinary(8)**|Endereço de memória do agendador. Para obter mais informações, consulte [sys.DM os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|processor_group|**smallint**|Armazena a ID do grupo de processador que é atribuída a este thread.|  
|pdw_node_id|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="remarks"></a>Remarks  
 Se o estado do trabalhador for RUNNING e ele estiver em execução de modo não preemptivo, o endereço do trabalhador corresponderá ao active_worker_address em sys.dm_os_schedulers.  
  
 Quando um trabalhador que está esperando um evento é sinalizado, o trabalhador é colocado no início da fila executável. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que isso aconteça mil vezes em uma linha; depois disso o trabalhador é colocado no final da fila. Mover um trabalhador para o final da fila tem algumas implicações de desempenho.  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="examples"></a>Exemplos  
 Você pode usar a consulta a seguir para descobrir por quanto tempo um trabalhador esteve em execução em um estado SUSPENDED ou RUNNABLE.  
  
```sql
SELECT   
    t1.session_id,  
    CONVERT(varchar(10), t1.status) AS status,  
    CONVERT(varchar(15), t1.command) AS command,  
    CONVERT(varchar(10), t2.state) AS worker_state,  
    w_suspended =   
      CASE t2.wait_started_ms_ticks  
        WHEN 0 THEN 0  
        ELSE   
          t3.ms_ticks - t2.wait_started_ms_ticks  
      END,  
    w_runnable =   
      CASE t2.wait_resumed_ms_ticks  
        WHEN 0 THEN 0  
        ELSE   
          t3.ms_ticks - t2.wait_resumed_ms_ticks  
      END  
  FROM sys.dm_exec_requests AS t1  
  INNER JOIN sys.dm_os_workers AS t2  
    ON t2.task_address = t1.task_address  
  CROSS JOIN sys.dm_os_sys_info AS t3  
  WHERE t1.scheduler_id IS NOT NULL;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
 session_id status     command         worker_state w_suspended w_runnable  
 ---------- ---------- --------------- ------------ ----------- --------------------  
 4          background LAZY WRITER     SUSPENDED    688         688  
 6          background LOCK MONITOR    SUSPENDED    4657        4657
 19         background BRKR TASK       SUSPENDED    603820344   603820344  
 14         background BRKR EVENT HNDL SUSPENDED    63583641    63583641  
 51         running    SELECT          RUNNING      0           0  
 2          background RESOURCE MONITO RUNNING      0           603825954  
 3          background LAZY WRITER     SUSPENDED    422         422  
 7          background SIGNAL HANDLER  SUSPENDED    603820485   603820485  
 13         background TASK MANAGER    SUSPENDED    603824704   603824704  
 18         background BRKR TASK       SUSPENDED    603820407   603820407  
 9          background TRACE QUEUE TAS SUSPENDED    454         454  
 52         suspended  SELECT          SUSPENDED    35094       35094  
 1          background RESOURCE MONITO RUNNING      0           603825954  
```

 Na saída, quando `w_runnable` e `w_suspended` forem iguais, isto representará o tempo que o trabalhador se encontra no estado SUSPENDED. Caso contrário, `w_runnable` representará o tempo gasto pelo trabalhador no estado RUNNABLE. Na saída, a sessão `52` está `SUSPENDED` durante `35,094` milissegundos.  
  
## <a name="see-also"></a>Consulte também  
 [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


