---
title: sys. dm _os_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 822f4fea2764c6420da731845e8defc05807d3cf
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72261660"
---
# <a name="sysdm_os_workers-transact-sql"></a>sys.dm_os_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada trabalhador no sistema. Para obter mais informações sobre os trabalhadores, consulte o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md). 
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **Sys. dm _pdw_nodes_os_workers**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|worker_address|**varbinary(8)**|Endereço de memória do trabalhador.|  
|status|**int**|Somente para uso interno.|  
|is_preemptive|**bit**|1 = o trabalhador está executando com agendamento preventivo. Qualquer trabalhador que esteja executando código externo será executado sob agendamento preemptivo.|  
|is_fiber|**bit**|1 = o trabalhador está executando com lightweight pooling. Para obter mais informações, consulte [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).|  
|is_sick|**bit**|1 = o trabalhador está preso tentando obter um bloqueio de giro. Se este bit estiver definido, isto pode indicar um problema com contenção em um objeto frequentemente acessado.|  
|is_in_cc_exception|**bit**|1 = atualmente o trabalhador está tratando uma exceção não relativa ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_fatal_exception|**bit**|Especifica se este trabalhador recebeu uma exceção fatal.|  
|is_inside_catch|**bit**|1 = atualmente o trabalhador está tratando uma exceção.|  
|is_in_polling_io_completion_routine|**bit**|1 = atualmente o trabalhador está executando uma rotina de conclusão de E/S para uma E/S pendente. Para obter mais informações, consulte [Sys. dm &#40;_IO_PENDING_IO_REQUESTS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-io-pending-io-requests-transact-sql.md).|  
|context_switch_count|**int**|Número de alternâncias de contexto do agendador executadas por este trabalhador.|  
|pending_io_count|**int**|Número de E/Ss físicas executadas por este trabalhador.|  
|pending_io_byte_count|**bigint**|Número total de bytes para todas as E/Ss físicas pendentes para este trabalhador.|  
|pending_io_byte_average|**int**|Número médio de bytes das E/Ss físicas para este trabalhador.|  
|wait_started_ms_ticks|**bigint**|Pontual, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando esse operador entrou no estado suspenso. Subtrair esse valor de ms_ticks em [Sys. dm _os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) retorna o número de milissegundos que o trabalhador está esperando.|  
|wait_resumed_ms_ticks|**bigint**|Pontual, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando esse operador entrou no estado de executável. Subtrair esse valor de ms_ticks em [Sys. dm _os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) retorna o número de milissegundos que o trabalhador esteve na fila executável.|  
|task_bound_ms_ticks|**bigint**|Ponto no tempo, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando uma tarefa é associada a esse trabalhador.|  
|worker_created_ms_ticks|**bigint**|Ponto no tempo, em [ms_ticks](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), quando um trabalhador é criado.|  
|exception_num|**int**|Número do erro da última exceção que este trabalhador encontrou.|  
|exception_severity|**int**|Gravidade da última exceção que este trabalhador encontrou.|  
|exception_address|**varbinary(8)**|Endereço de código que lançou a exceção|  
|affinity|**bigint**|A afinidade do thread do trabalhador. Corresponde à afinidade do thread em [Sys. dm _os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md).|  
|state|**nvarchar(60)**|Estado do trabalhador. Pode ser um dos seguintes valores:<br /><br /> INIT = atualmente o trabalhador está sendo inicializado.<br /><br /> RUNNING = atualmente o trabalhador está executando de modo não preemptivo ou preemptivo.<br /><br /> RUNNABLE = o trabalhador está pronto para execução no agendador.<br /><br /> SUSPENDED = o trabalhador está atualmente suspenso, aguardando que um evento envie um sinal para ele.|  
|start_quantum|**bigint**|Tempo, em milissegundos, no início da execução atual deste trabalhador.|  
|end_quantum|**bigint**|Tempo, em milissegundos, no final da execução atual deste trabalhador.|  
|last_wait_type|**nvarchar(60)**|Tipo da última espera. Para obter uma lista de tipos de espera, consulte [Sys. &#40;DM _OS_WAIT_STATS Transact&#41;-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|return_code|**int**|Valor de retorno da última espera. Pode ser um dos seguintes valores:<br /><br /> 0 =SUCCESS<br /><br /> 3 = DEADLOCK<br /><br /> 4 = PREMATURE_WAKEUP<br /><br /> 258 = TIMEOUT|  
|quantum_used|**bigint**|Somente para uso interno.|  
|max_quantum|**bigint**|Somente para uso interno.|  
|boost_count|**int**|Somente para uso interno.|  
|tasks_processed_count|**int**|Número de tarefas que este trabalhador processou.|  
|fiber_address|**varbinary(8)**|Endereço de memória da fibra à qual este trabalhador está associado.<br /><br /> NULL = o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está configurado para lightweight pooling.|  
|task_address|**varbinary(8)**|Endereço de memória da tarefa atual. Para obter mais informações, consulte [Sys. dm &#40;_OS_TASKS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).|  
|memory_object_address|**varbinary(8)**|Endereço de memória do objeto de memória do trabalhador. Para obter mais informações, consulte [Sys. dm &#40;_OS_MEMORY_OBJECTS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).|  
|thread_address|**varbinary(8)**|Endereço de memória do thread associado a este trabalhador. Para obter mais informações, consulte [Sys. dm &#40;_OS_THREADS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md).|  
|signal_worker_address|**varbinary(8)**|Endereço de memória do trabalhador que sinalizou este objeto pela última vez. Para obter mais informações, consulte [Sys. dm _os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|scheduler_address|**varbinary(8)**|Endereço de memória do agendador. Para obter mais informações, consulte [Sys. dm &#40;_OS_SCHEDULERS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|processor_group|**smallint**|Armazena a ID do grupo de processador que é atribuída a este thread.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="remarks"></a>Comentários  
 Se o estado do trabalhador for RUNNING e ele estiver em execução de modo não preemptivo, o endereço do trabalhador corresponderá ao active_worker_address em sys.dm_os_schedulers.  
  
 Quando um trabalhador que está esperando um evento é sinalizado, o trabalhador é colocado no início da fila executável. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que isso aconteça mil vezes em uma linha; depois disso o trabalhador é colocado no final da fila. Mover um trabalhador para o final da fila tem algumas implicações de desempenho.  
  
## <a name="permissions"></a>Permissões

No [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer a permissão `VIEW SERVER STATE`.   
Nas camadas Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], o requer a permissão `VIEW DATABASE STATE` no banco de dados. Nas camadas Standard e Basic [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

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
 [SQL Server exibições &#40;&#41;de gerenciamento dinâmico relacionadas ao sistema operacional](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)       
 [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md#DOP)       
 [Guia de arquitetura de thread e tarefa](../../relational-databases/thread-and-task-architecture-guide.md)    
