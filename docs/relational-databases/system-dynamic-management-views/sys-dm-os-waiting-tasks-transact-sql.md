---
title: sys. dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cd7cab9ed1edc9a62398c119b3b5cc72006c5af
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734460"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Retorna informações sobre a fila de espera de tarefas que estão esperando algum recurso. Para obter mais informações sobre tarefas, consulte o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).
   
> [!NOTE]  
> Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_os_waiting_tasks**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary (8)**|Endereço da tarefa de espera.|  
|**session_id**|**smallint**|ID da sessão associada à tarefa.|  
|**exec_context_id**|**int**|ID do contexto de execução associado à tarefa.|  
|**wait_duration_ms**|**bigint**|Tempo de espera total para esse tipo, em milissegundos. Esse tempo é inclusivo do **signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Nome do tipo de espera.|  
|**resource_address**|**varbinary (8)**|Endereço do recurso pelo qual a tarefa está esperando.|  
|**blocking_task_address**|**varbinary (8)**|Tarefa que está mantendo esse recurso atualmente|  
|**blocking_session_id**|**smallint**|ID da sessão que está bloqueando a solicitação. Se esta coluna for NULL, a solicitação não estará bloqueada ou as informações da sessão de bloqueio não estarão disponíveis (ou não podem ser identificadas).<br /><br /> -2 = O recurso de bloqueio pertence a uma transação distribuída órfã.<br /><br /> -3 = O recurso de bloqueio pertence a uma transação de recuperação adiada.<br /><br /> -4 = A ID da sessão do proprietário da trava de bloqueio não pôde ser determinada devido a transições internas de estado da trava.|  
|**blocking_exec_context_id**|**int**|ID do contexto de execução da tarefa de bloqueio.|  
|**resource_description**|**nvarchar (3072)**|Descrição do recurso que está sendo consumido. Para obter mais informações, consulte a lista a seguir.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="resource_description-column"></a>Coluna resource_description  
 A coluna resource_description tem os valores possíveis a seguir.  
  
 **Proprietário do recurso de pool de threads:**  
  
-   ID do ThreadPool = Agendador\<hex-address>  
  
 **Proprietário do recurso de consulta paralela:**  
  
-   ID de exchangeEvent = {porta | Pipe} \<hex-address> waittype = \<exchange-wait-type> NodeId =\<exchange-node-id>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Proprietário do recurso de bloqueio:**  
  
-   \<type-specific-description>ID = modo de bloqueio \<lock-hex-address> = \<mode> associatedObjectId =\<associated-obj-id>  
  
     **\<type-specific-description>pode ser:**  
  
    -   Para o banco de dados: databaselock subresource = \<databaselock-subresource> DBID =\<db-id>  
  
    -   Para o arquivo: filelock FileID = \<file-id> subresource = \<filelock-subresource> DBID =\<db-id>  
  
    -   Para objeto: objectlock lockPartition = \<lock-partition-id> objID = \<obj-id> subresource = \<objectlock-subresource> DBID =\<db-id>  
  
    -   Para a página: PageLock FileID = \<file-id> PageId = \<page-id> DBID = \<db-id> subresource =\<pagelock-subresource>  
  
    -   Para a chave: Keylock hobtid = \<hobt-id> DBID =\<db-id>  
  
    -   Para extensão: extentlock FileID = \<file-id> PageId = \<page-id> DBID =\<db-id>  
  
    -   Para RID: ridlock FileID = \<file-id> PageId = \<page-id> DBID =\<db-id>  
  
    -   Para o aplicativo: applicationlock hash = \<hash> databasePrincipalId = \<role-id> DBID =\<db-id>  
  
    -   Para metadados: metadatalock subresource = \<metadata-subresource> ClassID = \<metadatalock-description> DBID =\<db-id>  
  
    -   Para HOBT: hobtlock hobtid = \<hobt-id> subresource = \<hobt-subresource> DBID =\<db-id>  
  
    -   Para ALLOCATION_UNIT: allocunitlock hobtid = \<hobt-id> subresource = \<alloc-unit-subresource> DBID =\<db-id>  
  
     **\<mode>pode ser:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Proprietário do recurso externo:**  
  
-   ExternalResource externo =\<wait-type>  
  
 **Proprietário do recurso genérico:**  
  
-   TransactionMutex TransactionInfo espaço de trabalho =\<workspace-id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Proprietário do recurso de trava:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID>  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
 
## <a name="example"></a>Exemplo
### <a name="a-identify-tasks-from-blocked-sessions"></a>a. Identificar tarefas de sessões bloqueadas. 

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
```   

### <a name="b-view-waiting-tasks-per-connection"></a>B. Exibir tarefas em espera por conexão

```sql
SELECT st.text AS [SQL Text], c.connection_id, w.session_id, 
  w.wait_duration_ms, w.wait_type, w.resource_address, 
  w.blocking_session_id, w.resource_description, c.client_net_address, c.connect_time
FROM sys.dm_os_waiting_tasks AS w
INNER JOIN sys.dm_exec_connections AS c ON w.session_id = c.session_id 
CROSS APPLY (SELECT * FROM sys.dm_exec_sql_text(c.most_recent_sql_handle)) AS st 
              WHERE w.session_id > 50 AND w.wait_duration_ms > 0
ORDER BY c.connection_id, w.session_id
GO
```

### <a name="c-view-waiting-tasks-for-all-user-processes-with-additional-information"></a>C. Exibir tarefas em espera para todos os processos de usuário com informações adicionais

```sql
SELECT 'Waiting_tasks' AS [Information], owt.session_id,
    owt.wait_duration_ms, owt.wait_type, owt.blocking_session_id,
    owt.resource_description, es.program_name, est.text,
    est.dbid, eqp.query_plan, er.database_id, es.cpu_time,
    es.memory_usage*8 AS memory_usage_KB
FROM sys.dm_os_waiting_tasks owt
INNER JOIN sys.dm_exec_sessions es ON owt.session_id = es.session_id
INNER JOIN sys.dm_exec_requests er ON es.session_id = er.session_id
OUTER APPLY sys.dm_exec_sql_text (er.sql_handle) est
OUTER APPLY sys.dm_exec_query_plan (er.plan_handle) eqp
WHERE es.is_user_process = 1
ORDER BY owt.session_id;
GO
```
  
## <a name="see-also"></a>Consulte Também  
[SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
