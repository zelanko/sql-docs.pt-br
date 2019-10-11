---
title: sys.dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0a89a48fa960812ee955cd3b7ecb30069161f61
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260384"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre a fila de espera de tarefas que estão esperando algum recurso. Para obter mais informações sobre tarefas, consulte o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).
   
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **Sys. dm _pdw_nodes_os_waiting_tasks**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|Endereço da tarefa de espera.|  
|**session_id**|**smallint**|ID da sessão associada à tarefa.|  
|**exec_context_id**|**int**|ID do contexto de execução associado à tarefa.|  
|**wait_duration_ms**|**bigint**|Tempo de espera total para esse tipo, em milissegundos. Esse tempo é inclusivo do **signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Nome do tipo de espera.|  
|**resource_address**|**varbinary(8)**|Endereço do recurso pelo qual a tarefa está esperando.|  
|**blocking_task_address**|**varbinary(8)**|Tarefa que está mantendo esse recurso atualmente|  
|**blocking_session_id**|**smallint**|ID da sessão que está bloqueando a solicitação. Se esta coluna for NULL, a solicitação não estará bloqueada ou as informações da sessão de bloqueio não estarão disponíveis (ou não podem ser identificadas).<br /><br /> -2 = O recurso de bloqueio pertence a uma transação distribuída órfã.<br /><br /> -3 = O recurso de bloqueio pertence a uma transação de recuperação adiada.<br /><br /> -4 = A ID da sessão do proprietário da trava de bloqueio não pôde ser determinada devido a transições internas de estado da trava.|  
|**blocking_exec_context_id**|**int**|ID do contexto de execução da tarefa de bloqueio.|  
|**resource_description**|**nvarchar(3072)**|Descrição do recurso que está sendo consumido. Para obter mais informações, consulte a lista a seguir.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="resource_description-column"></a>Coluna resource_description  
 A coluna resource_description tem os seguintes valores possíveis.  
  
 **Proprietário do recurso do pool de threads:**  
  
-   ID do ThreadPool = Scheduler @ no__t-0hex-address >  
  
 **Proprietário do recurso de consulta paralela:**  
  
-   exchangeEvent id={Port|Pipe}\<hex-address> WaitType=\<exchange-wait-type> nodeId=\<exchange-node-id>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Bloquear proprietário do recurso:**  
  
-   \<type-específico-Descrição > ID = Lock @ no__t-1lock-hex-address > Mode = \<mode > associatedObjectId = \<associated-obj-ID >  
  
     **os > de descrição \<type-specific podem ser:**  
  
    -   Para o banco de dados: databaselock subresource = \<databaselock-subresource > DBID = \<dB-ID >  
  
    -   Para o arquivo: filelock FileID = \<file-ID > subresource = \<filelock-subresource > DBID = \<dB-ID >  
  
    -   Para o objeto: objectlock lockPartition = \<lock-Partition-ID > objID = \<obj-ID > subresource = \<objectlock-subresource > DBID = \<dB-ID >  
  
    -   Para a página: PageLock FileID = \<file-ID > PageId = \<Page-ID > DBID = \<dB-ID > underresource = \<pagelock-subresource >  
  
    -   Para a chave: Keylock hobtid = \<hobt-ID > DBID = \<dB-ID >  
  
    -   Para extensão: extentlock FileID = \<file-ID > PageId = \<Page-ID > DBID = \<dB-ID >  
  
    -   Para RID: ridlock FileID = \<file-ID > PageId = \<Page-ID > DBID = \<dB-ID >  
  
    -   Para o aplicativo: applicationlock hash = \<hash > databasePrincipalId = \<role-ID > DBID = \<dB-ID >  
  
    -   Para metadados: metadatalock subresource = \<metadata-subresource > ClassID = \<metadatalock-Description > DBID = \<dB-ID >  
  
    -   Para HOBT: hobtlock hobtid = \<hobt-ID > subresource = \<hobt-subresource > DBID = \<dB-ID >  
  
    -   Para ALLOCATION_UNIT: allocunitlock hobtid = \<hobt-ID > subresource = \<alloc-Unit-subresource > DBID = \<dB-ID >  
  
     **\<mode > pode ser:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Proprietário do recurso externo:**  
  
-   ExternalResource externo = @no__t-tipo de 0wait >  
  
 **Proprietário do recurso genérico:**  
  
-   TransactionMutex TransactionInfo Workspace=\<workspace-id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Proprietário do recurso de trava:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID >  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>Permissões

No [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer a permissão `VIEW SERVER STATE`.   
Nas camadas Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], o requer a permissão `VIEW DATABASE STATE` no banco de dados. Nas camadas Standard e Basic [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
 
## <a name="example"></a>Exemplo
Este exemplo identificará as sessões bloqueadas. Execute a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Consulte também  
[SQL Server exibições &#40;&#41;de gerenciamento dinâmico relacionadas ao sistema operacional](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[Guia de arquitetura de thread e tarefa](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
