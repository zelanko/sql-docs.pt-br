---
description: sys.dm_exec_query_memory_grants (Transact-SQL)
title: sys. dm_exec_query_memory_grants (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/19/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_memory_grants_TSQL
- sys.dm_exec_query_memory_grants
- sys.dm_exec_query_memory_grants_TSQL
- dm_exec_query_memory_grants
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_memory_grants dynamic management view
ms.assetid: 2c417747-2edd-4e0d-8a9c-e5f445985c1a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da496a91a9ed3fa6a391d0862de7eb7fde391480
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546581"
---
# <a name="sysdm_exec_query_memory_grants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações sobre todas as consultas que foram solicitadas e estão aguardando uma concessão de memória ou recebeu uma concessão de memória. As consultas que não exigem uma concessão de memória não aparecerão nessa exibição. Por exemplo, as operações Sort e hash Join têm concessões de memória para a execução da consulta, enquanto as consultas sem uma cláusula **order by** não terão uma concessão de memória.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas. Além disso, os valores nas colunas **scheduler_id**, **wait_order**, **pool_id** **group_id** são filtrados; o valor da coluna é definido como nulo.  
  
> [!NOTE]  
> Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_exec_query_memory_grants**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|ID (SPID) da sessão em que esta consulta está em execução.|  
|**request_id**|**int**|ID da solicitação. Exclusiva no contexto da sessão.|  
|**scheduler_id**|**int**|ID do agendador que está programando esta consulta.|  
|**dop**|**smallint**|Grau de paralelismo desta consulta.|  
|**request_time**|**datetime**|Data e hora quando esta consulta solicitou a concessão de memória.|  
|**grant_time**|**datetime**|Data e hora quando a memória foi concedida a esta consulta. NULL se memória ainda não tiver sido concedida.|  
|**requested_memory_kb**|**bigint**|Quantidade total solicitada de memória em quilobytes.|  
|**granted_memory_kb**|**bigint**|Total de memória realmente concedido em quilobytes. Poderá ser NULL se a memória ainda não tiver sido concedida. Em uma situação típica, este valor deveria ser igual a **requested_memory_kb**. Na criação de índices, o servidor pode permitir memória sob demanda adicional além da memória inicialmente concedida.|  
|**required_memory_kb**|**bigint**|Memória mínima exigida para executar esta consulta em quilobytes. **requested_memory_kb** é igual ou maior que esse valor.|  
|**used_memory_kb**|**bigint**|Memória física usada neste momento em quilobytes.|  
|**max_used_memory_kb**|**bigint**|Máximo de memória física usada até este momento em quilobytes.|  
|**query_cost**|**float**|Custo de consulta estimado.|  
|**timeout_sec**|**int**|Tempo limite em segundos antes de esta consulta desistir da solicitação de concessão de memória.|  
|**resource_semaphore_id**|**smallint**|ID não exclusivo do semáforo do recurso no qual esta consulta está aguardando.<br /><br /> **Observação:** Essa ID é exclusiva em versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] . Essa alteração pode afetar a execução de consulta de solução de problemas. Para obter mais informações, consulte "Comentários", posteriormente neste tópico.|  
|**queue_id**|**smallint**|ID da fila de espera em que esta consulta aguarda concessões de memória. NULL se a memória já tiver sido concedida.|  
|**wait_order**|**int**|Ordem sequencial de consultas de espera dentro da **queue_id** especificada. Esse valor pode ser alterado para uma determinada consulta se outras consultas obtiverem concessões de memória ou atingirem o tempo limite. NULL se a memória já tiver sido concedida.|  
|**is_next_candidate**|**bit**|Candidato para a próxima concessão de memória.<br /><br /> 1 = Sim<br /><br /> 0 = Não<br /><br /> NULL = Se a memória já tiver sido concedida.|  
|**wait_time_ms**|**bigint**|Tempo de espera em milissegundos. NULL se a memória já tiver sido concedida.|  
|**plan_handle**|**varbinary(64)**|Identificador para este plano de consulta. Use **sys.dm_exec_query_plan** para extrair o plano XML real.|  
|**sql_handle**|**varbinary(64)**|Identificador de texto [!INCLUDE[tsql](../../includes/tsql-md.md)] desta consulta. Use **sys.dm_exec_sql_text** para obter o texto [!INCLUDE[tsql](../../includes/tsql-md.md)] real.|  
|**group_id**|**int**|ID do grupo de carga de trabalho em que esta consulta está sendo executada.|  
|**pool_id**|**int**|ID do pool de recursos a que este grupo de carga de trabalho pertence.|  
|**is_small**|**tinyint**|Quando definido como 1, indica que esta concessão usa o sinal do recurso pequeno. Quando definido como 0, indica que um sinal normal é usado.|  
|**ideal_memory_kb**|**bigint**|Tamanho, em quilobytes (KB), da concessão de memória para ajustar tudo na memória física. Ele tem como base a estimativa de cardinalidade.|  
|**pdw_node_id**|**int**|O identificador do nó em que essa distribuição está.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
|**reserved_worker_count**|**bigint**|Número de [threads de trabalho](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling)reservados.<br /><br />**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] |  
|**used_worker_count**|**bigint**|Número de [threads de trabalho](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling) usados neste momento.<br /><br />**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**max_used_worker_count**|**bigint**|Número máximo de [threads de trabalho](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling) usados até este momento.<br /><br />**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**reserved_node_bitmap**|**bigint**|Bitmap de nós NUMA em que os [threads de trabalho](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling) são reservados.<br /><br />**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], requer a permissão `VIEW DATABASE STATE` no banco de dados.   
   
## <a name="remarks"></a>Comentários  
 Um cenário de depuração típico para tempo limite de consulta pode se parecer com este:  
  
-   Verifique o status geral da memória do sistema usando [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md), [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) e vários contadores de desempenho.  
  
-   Verifique se há reservas de memória de execução da consulta em **sys.dm_os_memory_clerks**, em que `type = 'MEMORYCLERK_SQLQERESERVATIONS'`.  
  
-   Verifique se há consultas aguardando<sup>1</sup> para concessões usando **Sys. dm_exec_query_memory_grants**.  
  
    ```sql  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
    
    <sup>1</sup> Nesse cenário, o tipo de espera costuma ser RESOURCE_SEMAPHORE. Para obter mais informações, confira [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). 
  
-   Pesquisar cache para consultas com concessões de memória usando [Sys. dm_exec_cached_plans &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) e [sys. dm_exec_query_plan &#40;transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```sql  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
    ```  
  
-   Além disso, examine as consultas que usam bastante memória utilizando [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).  
  
    ```sql  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
      plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
    ```  
  
-   Se houver suspeita de uma consulta sem controle, examine o Plano de execução de [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) e o texto em lote de [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 As consultas que usam exibições de gerenciamento dinâmico que incluem `ORDER BY` ou agregações podem aumentar o consumo de memória e, portanto, contribuir para o problema que estão Solucionando problemas.  
  
 O recurso Administrador de Recursos permite que um administrador de banco de dados distribua recursos de servidor entre pools de recursos, até um máximo de 64 pools. A partir [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] do, cada pool se comporta como uma instância de servidor independente pequena e requer 2 semáforos. O número de linhas retornadas de **Sys. dm_exec_query_resource_semaphores** pode ser até 20 vezes mais do que as linhas retornadas em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_exec_query_resource_semaphores &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
 [Guia de arquitetura de thread e tarefa](../../relational-databases/thread-and-task-architecture-guide.md)   
  
