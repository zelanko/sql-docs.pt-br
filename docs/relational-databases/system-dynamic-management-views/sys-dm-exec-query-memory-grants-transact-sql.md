---
title: sys.dm_exec_query_memory_grants (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2332e4f80e0dded930b22d9f0faf76d80ec09141
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013230"
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre todas as consultas que solicitaram e estão aguardando uma concessão de memória ou ter recebido uma concessão de memória. Consultas que não exigem uma concessão de memória não aparecerão nessa exibição. Por exemplo, classificar e operações de junção de hash têm concessões de memória para execução da consulta, enquanto consultas sem um **ORDER BY** cláusula não terá uma memória conceder.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém dados que não pertencem ao locatário conectado será filtrada. Além disso, os valores nas colunas **scheduler_id**, **wait_order**, **pool_id**, **group_id** são filtrados; o valor da coluna está definido como NULL.  
  
> [!NOTE]  
> Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_exec_query_memory_grants**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|ID (SPID) da sessão em que esta consulta está em execução.|  
|**request_id**|**int**|ID da solicitação. Exclusiva no contexto da sessão.|  
|**scheduler_id**|**int**|ID do agendador que está programando esta consulta.|  
|**dop**|**smallint**|Grau de paralelismo desta consulta.|  
|**request_time**|**datetime**|Data e hora quando esta consulta solicitou a concessão de memória.|  
|**grant_time**|**datetime**|Data e hora quando a memória foi concedida a esta consulta. NULL se memória ainda não tiver sido concedida.|  
|**requested_memory_kb**|**bigint**|Quantidade total solicitada de memória em quilobytes.|  
|**granted_memory_kb**|**bigint**|Total de memória realmente concedido em quilobytes. Poderá ser NULL se a memória ainda não tiver sido concedida. Uma situação típica, esse valor deve ser igual **requested_memory_kb**. Na criação de índices, o servidor pode permitir memória sob demanda adicional além da memória inicialmente concedida.|  
|**required_memory_kb**|**bigint**|Memória mínima exigida para executar esta consulta em quilobytes. **requested_memory_kb** é igual ou maior do que esse valor.|  
|**used_memory_kb**|**bigint**|Memória física usada neste momento em quilobytes.|  
|**max_used_memory_kb**|**bigint**|Máximo de memória física usada até este momento em quilobytes.|  
|**query_cost**|**float**|Custo de consulta estimado.|  
|**timeout_sec**|**int**|Tempo limite em segundos antes de esta consulta desistir da solicitação de concessão de memória.|  
|**resource_semaphore_id**|**smallint**|ID não exclusivo do semáforo do recurso no qual esta consulta está aguardando.<br /><br /> **Observação:** Essa ID é exclusiva em versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Essa alteração pode afetar a execução de consulta de solução de problemas. Para obter mais informações, consulte "Comentários", posteriormente neste tópico.|  
|**queue_id**|**smallint**|ID da fila de espera em que esta consulta aguarda concessões de memória. NULL se a memória já tiver sido concedida.|  
|**wait_order**|**int**|Ordem sequencial das consultas de espera dentro do especificado **queue_id**. Esse valor pode mudar para uma determinada consulta se outras consultas obtiverem concessões de memória ou tempo limite. NULL se a memória já tiver sido concedida.|  
|**is_next_candidate**|**bit**|Candidato para a próxima concessão de memória.<br /><br /> 1 = Sim<br /><br /> 0 = Não<br /><br /> NULL = Se a memória já tiver sido concedida.|  
|**wait_time_ms**|**bigint**|Tempo de espera em milissegundos. NULL se a memória já tiver sido concedida.|  
|**plan_handle**|**varbinary(64)**|Identificador para este plano de consulta. Use **. DM exec_query_plan** para extrair o plano XML real.|  
|**sql_handle**|**varbinary(64)**|Identificador de texto [!INCLUDE[tsql](../../includes/tsql-md.md)] desta consulta. Use **DM exec_sql_text** para obter o valor real [!INCLUDE[tsql](../../includes/tsql-md.md)] texto.|  
|**group_id**|**int**|ID do grupo de carga de trabalho em que esta consulta está sendo executada.|  
|**pool_id**|**int**|ID do pool de recursos a que este grupo de carga de trabalho pertence.|  
|**is_small**|**tinyint**|Quando definido como 1, indica que esta concessão usa o sinal do recurso pequeno. Quando definido como 0, indica que um sinal normal é usado.|  
|**ideal_memory_kb**|**bigint**|Tamanho, em quilobytes (KB), da concessão de memória para ajustar tudo na memória física. Ele tem como base a estimativa de cardinalidade.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   
   
## <a name="remarks"></a>Comentários  
 Um cenário de depuração típico para tempo limite de consulta pode se parecer com este:  
  
-   Verificar o uso de status de memória de sistema geral [DM os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md), [DM os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)e vários contadores de desempenho.  
  
-   Verificar se há reservas de memória de execução da consulta em **DM os_memory_clerks** onde `type = 'MEMORYCLERK_SQLQERESERVATIONS'`.  
  
-   Verificar se há consultas aguardando<sup>1</sup> para concessões que usam **DM exec_query_memory_grants**.  
  
    ```sql  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
    
    <sup>1</sup> Nesse cenário, o tipo de espera costuma ser RESOURCE_SEMAPHORE. Para obter mais informações, confira [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). 
  
-   Cache para consultas de pesquisa com concessões de memória usando [DM exec_cached_plans &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) e [. DM exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```sql  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
    ```  
  
-   Além disso, examine consultas intensivo de memória usando [. DM exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).  
  
    ```sql  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
      plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
    ```  
  
-   Se houver suspeita de uma consulta de fuga, examine o plano de execução de [. DM exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) e texto em lote de [DM exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 Consultas que usam exibições de gerenciamento dinâmico que incluem `ORDER BY` ou agregações podem aumentar o consumo de memória e, portanto, contribuem para o solução do problema.  
  
 O recurso Administrador de Recursos permite que um administrador de banco de dados distribua recursos de servidor entre pools de recursos, até um máximo de 64 pools. Começando com [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], cada pool se comporta como uma instância de servidor independente pequena e requer 2 semáforos. O número de linhas retornadas de **DM exec_query_resource_semaphores** pode ser até 20 vezes mais do que as linhas que são retornadas em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_exec_query_resource_semaphores &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
