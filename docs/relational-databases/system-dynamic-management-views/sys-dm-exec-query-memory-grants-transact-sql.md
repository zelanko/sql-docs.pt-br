---
title: sys.dm_exec_query_memory_grants (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5ea497514e558ab362429c3c8dda880fd41570df
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre todas as consultas que solicitou e estão aguardando uma concessão de memória ou recebeu uma concessão de memória. As consultas que não exigem uma concessão de memória não aparecerão nessa exibição. Por exemplo, classificar e operações de junção de hash têm concessões de memória para a execução de consulta, enquanto consultas sem um **ORDER BY** cláusula não terá uma memória conceder.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém os dados que não pertencem ao locatário conectado será filtrada. Além disso, os valores nas colunas **scheduler_id**, **wait_order**, **pool_id**, **group_id** são filtrados; o valor da coluna está definido como NULL.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_exec_query_memory_grants**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|ID (SPID) da sessão em que esta consulta está em execução.|  
|**request_id**|**Int**|ID da solicitação. Exclusiva no contexto da sessão.|  
|**scheduler_id**|**Int**|ID do agendador que está programando esta consulta.|  
|**dop**|**smallint**|Grau de paralelismo desta consulta.|  
|**request_time**|**datetime**|Data e hora quando esta consulta solicitou a concessão de memória.|  
|**grant_time**|**datetime**|Data e hora quando a memória foi concedida a esta consulta. NULL se memória ainda não tiver sido concedida.|  
|**requested_memory_kb**|**bigint**|Quantidade total solicitada de memória em quilobytes.|  
|**granted_memory_kb**|**bigint**|Total de memória realmente concedido em quilobytes. Poderá ser NULL se a memória ainda não tiver sido concedida. Em uma situação típica, esse valor deve ser o mesmo que **requested_memory_kb**. Na criação de índices, o servidor pode permitir memória sob demanda adicional além da memória inicialmente concedida.|  
|**required_memory_kb**|**bigint**|Memória mínima exigida para executar esta consulta em quilobytes. **requested_memory_kb** é igual ou maior que esse valor.|  
|**used_memory_kb**|**bigint**|Memória física usada neste momento em quilobytes.|  
|**max_used_memory_kb**|**bigint**|Máximo de memória física usada até este momento em quilobytes.|  
|**query_cost**|**float**|Custo de consulta estimado.|  
|**timeout_sec**|**Int**|Tempo limite em segundos antes de esta consulta desistir da solicitação de concessão de memória.|  
|**resource_semaphore_id**|**smallint**|ID não exclusivo do semáforo do recurso no qual esta consulta está aguardando.<br /><br /> **Observação:** essa ID é exclusiva em versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Essa alteração pode afetar a execução de consulta de solução de problemas. Para obter mais informações, consulte "Comentários", posteriormente neste tópico.|  
|**queue_id**|**smallint**|ID da fila de espera em que esta consulta aguarda concessões de memória. NULL se a memória já tiver sido concedida.|  
|**wait_order**|**Int**|Ordem sequencial de consultas de espera em especificado **queue_id**. Esse valor poderá ser alterado para uma determinada consulta se outras consultas obtiverem concessões de memória ou tempo limite. NULL se a memória já tiver sido concedida.|  
|**is_next_candidate**|**bit**|Candidato para a próxima concessão de memória.<br /><br /> 1 = Sim<br /><br /> 0 = Não<br /><br /> NULL = Se a memória já tiver sido concedida.|  
|**wait_time_ms**|**bigint**|Tempo de espera em milissegundos. NULL se a memória já tiver sido concedida.|  
|**plan_handle**|**varbinary(64)**|Identificador para este plano de consulta. Use **sys.DM exec_query_plan** para extrair o plano XML real.|  
|**sql_handle**|**varbinary(64)**|Identificador de texto [!INCLUDE[tsql](../../includes/tsql-md.md)] desta consulta. Use **dm_exec_sql_text** para obter o valor real [!INCLUDE[tsql](../../includes/tsql-md.md)] texto.|  
|**group_id**|**Int**|ID do grupo de carga de trabalho em que esta consulta está sendo executada.|  
|**pool_id**|**Int**|ID do pool de recursos a que este grupo de carga de trabalho pertence.|  
|**is_small**|**tinyint**|Quando definido como 1, indica que esta concessão usa o sinal do recurso pequeno. Quando definido como 0, indica que um sinal normal é usado.|  
|**ideal_memory_kb**|**bigint**|Tamanho, em quilobytes (KB), da concessão de memória para ajustar tudo na memória física. Ele tem como base a estimativa de cardinalidade.|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   
   
## <a name="remarks"></a>Remarks  
 Um cenário de depuração típico para tempo limite de consulta pode se parecer com este:  
  
-   Verifique o status geral sistema memória usando [sys.DM os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md), [sys.DM os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)e vários contadores de desempenho.  
  
-   Verificar se há reservas de memória de execução da consulta em **sys.DM os_memory_clerks** onde `type = 'MEMORYCLERK_SQLQERESERVATIONS'`.  
  
-   Verifique se há consultas aguardando concessões que usam **sys.DM exec_query_memory_grants**.  
  
    ```  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
  
-   Cache para consultas de pesquisa com concessões de memória usando[exec_cached_plans &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) e [sys.DM exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
  
    ```  
  
-   Além disso, examine as consultas de uso intensivo de memória usando [exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).  
  
    ```  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    Plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
  
    ```  
  
-   Se houver suspeita de uma consulta sem controle, examine o plano de execução de [sys.DM exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) e texto em lote de [dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 As consultas que usam exibições de gerenciamento dinâmico com ORDER BY ou agregações podem aumentar o uso da memória e, dessa forma, contribuir para a solução do problema.  
  
 O recurso Administrador de Recursos permite que um administrador de banco de dados distribua recursos de servidor entre pools de recursos, até um máximo de 64 pools. Começando com [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], cada pool se comporta como uma instância de servidor independente pequena e requer 2 semáforos. O número de linhas retornadas de **sys.DM exec_query_resource_semaphores** pode ser até 20 vezes mais do que as linhas que são retornadas em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_exec_query_resource_semaphores &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


