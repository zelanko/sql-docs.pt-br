---
title: sys.dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 914d26a40ea2c1c5f3246dd134e0888dddeff891
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmoswaitingtasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre a fila de espera de tarefas que estão esperando algum recurso.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_waiting_tasks**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|Endereço da tarefa de espera.|  
|**session_id**|**smallint**|ID da sessão associada à tarefa.|  
|**exec_context_id**|**Int**|ID do contexto de execução associado à tarefa.|  
|**wait_duration_ms**|**bigint**|Tempo de espera total para esse tipo, em milissegundos. Esse tempo é inclusivo do **signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Nome do tipo de espera.|  
|**resource_address**|**varbinary(8)**|Endereço do recurso pelo qual a tarefa está esperando.|  
|**blocking_task_address**|**varbinary(8)**|Tarefa que está mantendo esse recurso atualmente|  
|**blocking_session_id**|**smallint**|ID da sessão que está bloqueando a solicitação. Se esta coluna for NULL, a solicitação não estará bloqueada ou as informações da sessão de bloqueio não estarão disponíveis (ou não podem ser identificadas).<br /><br /> -2 = O recurso de bloqueio pertence a uma transação distribuída órfã.<br /><br /> -3 = O recurso de bloqueio pertence a uma transação de recuperação adiada.<br /><br /> -4 = A ID da sessão do proprietário da trava de bloqueio não pôde ser determinada devido a transições internas de estado da trava.|  
|**blocking_exec_context_id**|**Int**|ID do contexto de execução da tarefa de bloqueio.|  
|**resource_description**|**nvarchar(3072)**|Descrição do recurso que está sendo consumido. Para obter mais informações, consulte a lista a seguir.|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="resourcedescription-column"></a>Coluna resource_description  
 A coluna resource_description tem os seguintes valores possíveis.  
  
 **Proprietário do recurso de pool de threads:**  
  
-   id de ThreadPool = Agendador\<hex-address >  
  
 **Proprietário do recurso de consulta paralela:**  
  
-   exchangeEvent id = {porta | Pipe}\<hex-address > WaitType =\<exchange-wait-type > nodeId =\<exchange-node-id >  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Proprietário do recurso de bloqueio:**  
  
-   \<tipo-specific-description > id = bloqueio\<bloqueio-hex-address > modo =\<modo > associatedObjectId =\<associado-obj-id >  
  
     **\<tipo-specific-description > pode ser:**  
  
    -   Para o banco de dados: Databaselock subresource =\<databaselock-subresource > dbid =\<db-id >  
  
    -   Para um arquivo: Filelock fileid =\<arquivo-id > subresource =\<filelock-subresource > dbid =\<db-id >  
  
    -   Para OBJECT: Objectlock lockPartition =\<lock-partition-id > objid =\<obj-id > subresource =\<objectlock-subresource > dbid =\<db-id >  
  
    -   Para PAGE: Pagelock fileid =\<arquivo-id > pageid =\<id da página > dbid =\<db-id > subresource =\<pagelock-subresource >  
  
    -   Para Key: Keylock hobtid =\<hobt-id > dbid =\<db-id >  
  
    -   Para EXTENT: Extentlock fileid =\<arquivo-id > pageid =\<id da página > dbid =\<db-id >  
  
    -   Para RID: Ridlock fileid =\<arquivo-id > pageid =\<id da página > dbid =\<db-id >  
  
    -   Para APPLICATION: Applicationlock hash =\<hash > databasePrincipalId =\<função-id > dbid =\<db-id >  
  
    -   Para METADATA: Metadatalock subresource =\<metadados-subresource > classid =\<metadatalock-description > dbid =\<db-id >  
  
    -   Para HOBT: Hobtlock hobtid =\<hobt-id > subresource =\<hobt-subresource > dbid =\<db-id >  
  
    -   Para ALLOCATION_UNIT: Allocunitlock hobtid =\<hobt-id > subresource =\<alloc-unit-subresource > dbid =\<db-id >  
  
     **\<modo > pode ser:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Proprietário do recurso externo:**  
  
-   ExternalResource externo =\<tipo de espera >  
  
 **Proprietário do recurso genérico:**  
  
-   TransactionMutex TransactionInfo Workspace=\<workspace-id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Proprietário do recurso de trava:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID &GT;  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   
 
## <a name="example"></a>Exemplo
Este exemplo identificará as sessões bloqueadas.  Execute o [!INCLUDE[tsql](../../includes/tsql-md.md)] de consulta em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Consulte também  
  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


