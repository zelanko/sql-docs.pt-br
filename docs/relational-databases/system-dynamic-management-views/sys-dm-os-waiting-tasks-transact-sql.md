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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0a89a48fa960812ee955cd3b7ecb30069161f61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72260384"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre a fila de espera de tarefas que estão esperando algum recurso. Para obter mais informações sobre tarefas, consulte o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).
   
> [!NOTE]  
>  Para chamá-lo [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]ou, use o nome **Sys. dm_pdw_nodes_os_waiting_tasks**.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary (8)**|Endereço da tarefa de espera.|  
|**session_id**|**smallint**|ID da sessão associada à tarefa.|  
|**exec_context_id**|**int**|ID do contexto de execução associado à tarefa.|  
|**wait_duration_ms**|**bigint**|Tempo de espera total para esse tipo, em milissegundos. Esse tempo é inclusivo do **signal_wait_time**.|  
|**wait_type**|**nvarchar (60)**|Nome do tipo de espera.|  
|**resource_address**|**varbinary (8)**|Endereço do recurso pelo qual a tarefa está esperando.|  
|**blocking_task_address**|**varbinary (8)**|Tarefa que está mantendo esse recurso atualmente|  
|**blocking_session_id**|**smallint**|ID da sessão que está bloqueando a solicitação. Se esta coluna for NULL, a solicitação não estará bloqueada ou as informações da sessão de bloqueio não estarão disponíveis (ou não podem ser identificadas).<br /><br /> -2 = O recurso de bloqueio pertence a uma transação distribuída órfã.<br /><br /> -3 = O recurso de bloqueio pertence a uma transação de recuperação adiada.<br /><br /> -4 = A ID da sessão do proprietário da trava de bloqueio não pôde ser determinada devido a transições internas de estado da trava.|  
|**blocking_exec_context_id**|**int**|ID do contexto de execução da tarefa de bloqueio.|  
|**resource_description**|**nvarchar (3072)**|Descrição do recurso que está sendo consumido. Para obter mais informações, consulte a lista a seguir.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="resource_description-column"></a>Coluna resource_description  
 A coluna resource_description tem os valores possíveis a seguir.  
  
 **Proprietário do recurso de pool de threads:**  
  
-   ID do ThreadPool =>\<de endereço hexadecimal do Agendador  
  
 **Proprietário do recurso de consulta paralela:**  
  
-   ID de exchangeEvent = {porta | Pipe}\<endereço hex> waittype =\<troca de espera do Exchange> NodeId =\<Exchange-node-id>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Proprietário do recurso de bloqueio:**  
  
-   \<tipo-específico-Descrição> ID = Lock\<Lock-hex-address> mode =\<Mode> associatedObjectId =\<associado-obj-ID>  
  
     **\<a descrição de tipo específico> pode ser:**  
  
    -   Para o banco de dados: databaselock\<subresource = databaselock-subresource\<> DBID = DB-ID>  
  
    -   Para o arquivo: filelock FileID\<= ID-do-arquivo>\<o subrecurso = filelock-subresource> DBID =\<DB-ID>  
  
    -   Para OBJECT: objectlock lockPartition =\<Lock-Partition-ID> objID =\<obj-ID> subresource =\<objectlock-subresource> DBID =\<DB-ID>  
  
    -   Para a página: PageLock FileID\<= ID de arquivo> PageId\<= ID de página> DBID\<= DB-ID> subresource\<= PageLock-subresource>  
  
    -   Para a chave: Keylock hobtid\<= HoBT-ID> DBID\<= DB-ID>  
  
    -   Para extensão: extentlock FileID =\<File-ID> PageId =\<Page-ID> DBID =\<DB-ID>  
  
    -   Para RID: ridlock FileID =\<ID de arquivo> PageId =\<ID de página> DBID =\<DB-ID>  
  
    -   Para o aplicativo: applicationlock hash\<= hash> databasePrincipalId\<= ID de função> DBID\<= DB-ID>  
  
    -   Para metadados: metadatalock subresource =\<metadados-subresource> ClassID =\<metadatalock-Description> DBID =\<DB-ID>  
  
    -   Para HOBT: hobtlock hobtid =\<HoBT-ID> subresource =\<HOBT-subresource> DBID =\<DB-ID>  
  
    -   Para ALLOCATION_UNIT: allocunitlock hobtid =\<HoBT-ID> subresource =\<Alloc-UNIT-subresource> DBID =\<DB-ID>  
  
     **\<o modo> pode ser:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Proprietário do recurso externo:**  
  
-   ExternalResource externa =\<tipo de espera>  
  
 **Proprietário do recurso genérico:**  
  
-   TransactionMutex TransactionInfo Workspace =\<Workspace-ID>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Proprietário do recurso de trava:**  
  
-   \<DB-ID>:\<ID de arquivo>:\<página-in-file>  
  
-   \<GUID>  
  
-   \<> de classe de trava\<(> de trava-endereço)  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
 
## <a name="example"></a>Exemplo
Este exemplo identificará as sessões bloqueadas. Execute a [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Consulte Também  
[SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[Guia de arquitetura de thread e tarefa](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
