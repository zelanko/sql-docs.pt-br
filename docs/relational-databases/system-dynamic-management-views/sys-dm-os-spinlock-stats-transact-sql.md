---
title: sys.dm_os_spinlock_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats
- sys.dm_os_spinlock_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_spinlock_stats dynamic management view
author: bluefooted
ms.author: pamela
ms.reviewer: maghan
manager: amitban
ms.openlocfilehash: e302eadaa559674482911904678cc8aa4cbd2577
ms.sourcegitcommit: e366f702c49d184df15a9b93c2c6a610e88fa0fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67826606"
---
# <a name="sysdmosspinlockstats-transact-sql"></a>sys.dm_os_spinlock_stats (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna informações sobre todas as esperas de spinlock organizado por tipo.  
  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(256)**|Nome do tipo de spinlock.|  
|colisões|**bigint**|O número de vezes que um thread tenta adquirir o spinlock e está bloqueado porque outro thread atualmente mantém o spinlock.|  
|Gira|**bigint**|O número de vezes que um thread executa um loop ao tentar adquirir o spinlock.|  
|spins_per_collision|**real**|Taxa de rotações por colisão.|  
|sleep_time|**bigint**|A quantidade de tempo em milissegundos que o segmento gasto em suspensão no caso de uma retirada.|  
|retiradas|**int**|O número de vezes que um thread que está "girando" Falha ao adquirir o spinlock e produzir o Agendador.|  


## <a name="permissions"></a>Permissões  
Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` permissão no banco de dados. Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e básica, requer a **administrador de servidor** ou uma **administrador do Active Directory do Azure** conta.    
  
## <a name="remarks"></a>Comentários  
 
 sys.dm_os_spinlock_stats pode ser usado para identificar a origem da contenção de spinlock. Em algumas situações, talvez você possa resolver ou reduzir a contenção de spinlock. Entretanto, pode haver situações em que seja necessário contatar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Serviço de Atendimento ao Cliente.  
  
 Você pode redefinir o conteúdo de sys.dm_os_spinlock_stats usando `DBCC SQLPERF` da seguinte maneira:  
  
```  
DBCC SQLPERF ('sys.dm_os_spinlock_stats', CLEAR);  
GO  
```  
  
 Isso redefine todos os contadores como 0.  
  
> [!NOTE]  
>  Essas estatísticas não persistirão se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reiniciado. Todos os dados são acumulados desde a última vez em que as estatísticas foram redefinidas ou desde que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado.  
  
## <a name="spinlocks"></a>Spinlocks  
 Um spinlock é um objeto de sincronização leve usado para serializar o acesso a estruturas de dados que normalmente são mantidas por um curto período de tempo. Quando um thread tenta acessar um recurso protegido por um spinlock que está sendo mantido por outro thread, o thread executará um loop, ou "girar" e tentar acessar o recurso novamente, em vez de gerar imediatamente o Agendador com uma trava ou outro recurso Aguarde. O thread continuará a rotação até que o recurso está disponível ou o loop estiver concluído, momento em que o thread produzir o Agendador e Voltar na fila executável. Essa prática ajuda a reduzir a alternância de contexto excessiva thread, mas quando a contenção de um spinlock é alta, a utilização de CPU significativa pode ser observada.
   
 A tabela a seguir contém breves descrições de alguns dos tipos mais comuns de spinlock.  
  
|Tipo de spinlock|Descrição|  
|-----------------|-----------------|  
|ABR|Somente para uso interno.|
|ADB_CACHE|Somente para uso interno.|
|ALLOC_CACHES_HASH|Somente para uso interno.|
|APPENDONLY_STORAGE|Somente para uso interno.|
|APRC_BACK_OFF_STATS|Somente para uso interno.|
|APRC_EVENT_LIST|Somente para uso interno.|
|APRC_QUEUE_LIST|Somente para uso interno.|
|APRC_VALIDATION_QUEUE_LIST|Somente para uso interno.|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|Somente para uso interno.|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|Somente para uso interno.|
|ASYNCSTATSLIST|Somente para uso interno.|
|BACKUP|Somente para uso interno.|
|BACKUP_COPY_CONTEXT|Somente para uso interno.|
|BACKUP_CTX|Somente para uso interno.|
|BASE_XACT_HASH|Somente para uso interno.|
|BLOCKER_ENUM|Somente para uso interno.|
|BPREPARTITION|Somente para uso interno.|
|BPWORKFILE|Somente para uso interno.|
|BUF_HASH|Somente para uso interno.|
|BUF_LINK|Somente para uso interno.|
|BUF_WRITE_LOG|Somente para uso interno.|
|CACHEOBJ_DBG|Somente para uso interno.|
|CHANNELFORCECLOSEMANAGER|Somente para uso interno.|
|CHECK_AGGREGATE_STATE|Somente para uso interno.|
|CLR_HOSTTASK|Somente para uso interno.|
|CLR_SPIN_LOCK|Somente para uso interno.|
|CMED_DATABASE|Somente para uso interno.|
|CMED_HASH_SET|Somente para uso interno.|
|COLUMNDATASETSESSIONLIST|Somente para uso interno.|
|COLUMNSTORE_HASHTABLE|Somente para uso interno.|
|COLUMNSTOREBUILDSTATE_LIST|Somente para uso interno.|
|COM_INIT|Somente para uso interno.|
|PODE SER CONFIRMADA|Somente para uso interno.|
|COMPPLAN_SKELETON|Somente para uso interno.|
|CONNECTION_MANAGER|Somente para uso interno.|
|CONECTA-SE|Somente para uso interno.|
|CSIBUILDMEM|Somente para uso interno.|
|CURSOR|Somente para uso interno.|
|CURSQL|Somente para uso interno.|
|DATAPORTCONSUMER|Somente para uso interno.|
|DATAPORTSOURCEINFOCREDIT|Somente para uso interno.|
|DATAPORTSOURCEINFOQUEUE|Somente para uso interno.|
|DATASET_FREELIST|Somente para uso interno.|
|DBCC_CHECK|Somente para uso interno.|
|DBSEEDING_OPERATION|Somente para uso interno.|
|DBT_HASH|Somente para uso interno.|
|DBT_IO_LIST|Somente para uso interno.|
|DBTABLE|Controla o acesso a uma estrutura de dados na memória para cada banco de dados em um SQL Server que contém as propriedades do banco de dados. Ver [deste artigo](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789) para obter mais informações. |
|DEFERRED_WF_EXT_DROP|Somente para uso interno.|
|DEK_INSTANCE|Somente para uso interno.|
|DELAYED_PARTITIONED_STACK|Somente para uso interno.|
|DELETEBITMAP|Somente para uso interno.|
|DIAG_MANAGER|Somente para uso interno.|
|DIAG_OBJECT|Somente para uso interno.|
|DIGEST_CACHE|Somente para uso interno.|
|DINPBUF|Somente para uso interno.|
|DIRECTLOGCONSUMER|Somente para uso interno.|
|DP_LIST|Controla o acesso à lista de páginas sujas para um banco de dados que tem o ponto de verificação indireto ativado. Ver [deste artigo](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510) para obter mais informações.|
|DROP|Somente para uso interno.|
|DROP_TEMPO|Somente para uso interno.|
|DROPPED_ALLOC_UNIT|Somente para uso interno.|
|DTC_HASHTABLE|Somente para uso interno.|
|DTT_LIST|Somente para uso interno.|
|ENDD_LIST|Somente para uso interno.|
|EXT_CACHE|Somente para uso interno.|
|EXTENT_ACTIVATION|Somente para uso interno.|
|FABRIC_DB_MGR_PTR|Somente para uso interno.|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|Somente para uso interno.|
|FABRIC_REPLICA_TRANSPORT|Somente para uso interno.|
|FABRIC_TVF_DATA_CONSUMER_LIST|Somente para uso interno.|
|FABRIC_TVF_LOAD_LIB|Somente para uso interno.|
|FCB_REPLICA_SYNC|Somente para uso interno.|
|FGCB_PRP_FILL|Somente para uso interno.|
|FILE_HANDLE_CACHE|Somente para uso interno.|
|FILE_TABLE|Somente para uso interno.|
|FILESTREAM_CHUNKER|Somente para uso interno.|
|FREE_SPACE_CACHE_ENTRY|Somente para uso interno.|
|FS_CONTAINER_LIST_WITH_DELETE|Somente para uso interno.|
|FS_DELETED_FOLDER_CLEANUP|Somente para uso interno.|
|FSAGENT|Somente para uso interno.|
|FSGHOST_STATUS|Somente para uso interno.|
|FT_INIT|Somente para uso interno.|
|GHOST_FREE|Somente para uso interno.|
|GHOST_HASH|Somente para uso interno.|
|GLOBAL_SCHEDULER_LIST|Somente para uso interno.|
|GLOBAL_TRACE_FLAGS|Somente para uso interno.|
|GLOBALTRANS|Somente para uso interno.|
|GROUP_COMMIT_FEEDBACK_LOOP|Somente para uso interno.|
|GUARDIAN|Somente para uso interno.|
|HADR_AGH_X_ACCESS|Somente para uso interno.|
|HADR_AR_CONTROLLER_COLLECTION|Somente para uso interno.|
|HADR_AR_DB_MGR|Somente para uso interno.|
|HADR_AR_TRANSPORT|Somente para uso interno.|
|HADR_COMPRESSION_MGR_POOL|Somente para uso interno.|
|HADR_FABRIC_FACTORY|Somente para uso interno.|
|HADR_PRIORITY_QUEUE|Somente para uso interno.|
|HADR_TRANSPORT_CONTROL|Somente para uso interno.|
|HADR_TRANSPORT_LIST|Somente para uso interno.|
|HADRSEEDINGLIST|Somente para uso interno.|
|HOBT_DROPPED|Somente para uso interno.|
|HOBT_HASH|Somente para uso interno.|
|HTTP|Somente para uso interno.|
|HTTP_CONNCACHE|Somente para uso interno.|
|HTTP_ENDPOINT|Somente para uso interno.|
|IDENTITY|Somente para uso interno.|
|INDEX_CREATE|Somente para uso interno.|
|IO_DISPENSER_PAUSE|Somente para uso interno.|
|IO_RG_VOLUME_HASHTABLE|Somente para uso interno.|
|IOREQ|Somente para uso interno.|
|ISSRESOURCE|Somente para uso interno.|
|KTM_ENLISTMENT|Somente para uso interno.|
|LANG_RES_LOAD|Somente para uso interno.|
|LIVE_TARGET_TVF|Somente para uso interno.|
|LOCK_FREE_LIST|Somente para uso interno.|
|LOCK_HASH|Protege o acesso para a tabela de hash do Gerenciador de bloqueio que armazena informações sobre os bloqueios que estão sendo mantidos em um banco de dados. Ver [deste artigo](https://support.microsoft.com/kb/2926217) para obter mais informações.|
|LOCK_NOTIFICATION|Somente para uso interno.|
|LOCK_RESOURCE_ID|Somente para uso interno.|
|LOCK_RW_ABTX_HASH_SET|Somente para uso interno.|
|LOCK_RW_AGDB_HEALTH_DIAG|Somente para uso interno.|
|LOCK_RW_CMED_HASH_SET|Somente para uso interno.|
|LOCK_RW_DPT_TABLE|Somente para uso interno.|
|LOCK_RW_IN_ROW_TRACKER|Somente para uso interno.|
|LOCK_RW_LOGIN_RATE_STATS|Somente para uso interno.|
|LOCK_RW_PVS_PAGE_TRACKER|Somente para uso interno.|
|LOCK_RW_RBIO_REQ|Somente para uso interno.|
|LOCK_RW_SECURITY_CACHE|Somente para uso interno.|
|LOCK_RW_TEST|Somente para uso interno.|
|LOCK_RW_WPR_BUCKET|Somente para uso interno.|
|LOCK_SORT_STREAM|Somente para uso interno.|
|LOCK_SQLSATELLITE_MESSAGE|Somente para uso interno.|
|LOG_CONSOLIDATION|Somente para uso interno.|
|LOG_RG_GOVERNOR|Somente para uso interno.|
|LOGCACHE_ACCESS|Somente para uso interno.|
|LOGFLUSHQ|Somente para uso interno.|
|LOGIOSEQ|Somente para uso interno.|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|Somente para uso interno.|
|LOGLC|Somente para uso interno.|
|LOGLFM|Somente para uso interno.|
|LOGON_TRIGGER_CACHE|Somente para uso interno.|
|LOGPOOL_HASHBUCKET|Somente para uso interno.|
|LOGPOOL_REFCOUNTEDOBJECT|Somente para uso interno.|
|LOGPOOL_SHAREDCACHEBUFFER|Somente para uso interno.|
|LOGPOOL_SIZEPERRESOURCEPOOL|Somente para uso interno.|
|LPE_BATCH|Somente para uso interno.|
|LPE_SESSION|Somente para uso interno.|
|LPE_SXTP|Somente para uso interno.|
|LSID|Somente para uso interno.|
|LSLIST|Somente para uso interno.|
|LSNREFLIST|Somente para uso interno.|
|LSS_SYNC_DTC|Somente para uso interno.|
|MD_CHANGE_NOTIFICATION|Somente para uso interno.|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|Somente para uso interno.|
|MDB_REMOTE_SESSION_HASH_TABLE|Somente para uso interno.|
|MEM_MGR|Somente para uso interno.|
|MGR_CACHE|Somente para uso interno.|
|MIGRATION_BUF_LIST|Somente para uso interno.|
|NETCONN_ADDRESS|Somente para uso interno.|
|ONDEMAND_TASK|Somente para uso interno.|
|ONE_PROC_SIM_NODE_CONTEXT|Somente para uso interno.|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|Somente para uso interno.|
|ONE_PROC_SIM_REPLICA_CONTEXT|Somente para uso interno.|
|ONE_PROC_SIM_SERVICE_PARTITION|Somente para uso interno.|
|OPT_IDX_MISS_ID|Somente para uso interno.|
|OPT_IDX_MISS_KEY|Somente para uso interno.|
|OPT_IDX_STATS|Somente para uso interno.|
|OPT_INFO_MGR|Somente para uso interno.|
|PAGE_WORKITEMLIST|Somente para uso interno.|
|PAGECOPIER|Somente para uso interno.|
|PARALLELREDOCACHE|Somente para uso interno.|
|PARTITIONED_HEAP_FREE_LIST|Somente para uso interno.|
|PROGRESS_REPORT|Somente para uso interno.|
|QE_SHUTDOWN|Somente para uso interno.|
|QSCAN_CACHE|Somente para uso interno.|
|QUERY_EXEC_STATS|Somente para uso interno.|
|QUERY_STORE_ASYNC_PERSIST|Somente para uso interno.|
|QUERY_STORE_ASYNC_QUEUE_TLIST|Somente para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|Somente para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_STATS|Somente para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|Somente para uso interno.|
|QUERY_STORE_CURRENT_INTERVAL|Somente para uso interno.|
|QUERY_STORE_HT_CACHE|Somente para uso interno.|
|QUERY_STORE_LIST|Somente para uso interno.|
|QUERY_STORE_PLAN_COMP_AGG|Somente para uso interno.|
|QUERY_STORE_PLAN_LIST|Somente para uso interno.|
|QUERY_STORE_READ_ONLY_FLAGS|Somente para uso interno.|
|QUERY_STORE_SELF_AGG|Somente para uso interno.|
|QUERY_STORE_STMT_COMP_AGG|Somente para uso interno.|
|QUERYEXEC|Somente para uso interno.|
|QUERYSCAN|Somente para uso interno.|
|RANGE_GENERATION|Somente para uso interno.|
|READ_AHEAD|Somente para uso interno.|
|REDOMGRSTATE|Somente para uso interno.|
|REMOTE_SESSION_CACHE|Somente para uso interno.|
|REMOTEBLOCKIO|Somente para uso interno.|
|REMOTEOP|Somente para uso interno.|
|REPL_LOGREADER_HISTORY_CACHE|Somente para uso interno.|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|Somente para uso interno.|
|RESMANAGER|Somente para uso interno.|
|RECURSO|Somente para uso interno.|
|RESQUEUE|Somente para uso interno.|
|RFS_THREAD_QUEUE|Somente para uso interno.|
|RG_TIMER|Somente para uso interno.|
|ROWGROUP_VERSIONS|Somente para uso interno.|
|RPCCHANNELPOOL|Somente para uso interno.|
|RPCPACKAGE|Somente para uso interno.|
|RPCREQUESTORCONTEXT|Somente para uso interno.|
|RWLOCK_LAST|Somente para uso interno.|
|SATELLITE_CONNECTION|Somente para uso interno.|
|SBS_CLIENT_ENDPOINTS|Somente para uso interno.|
|SBS_CLIENT_REQUESTS|Somente para uso interno.|
|SBS_DISPATCH|Somente para uso interno.|
|SBS_PENDING|Somente para uso interno.|
|SBS_SERVER_XACT_TASK_PROXY|Somente para uso interno.|
|SBS_TRANSPORT|Somente para uso interno.|
|SBS_UCS_DISPATCH|Somente para uso interno.|
|SEGURANÇA|Somente para uso interno.|
|SECURITY_CACHE|Somente para uso interno.|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|Somente para uso interno.|
|SEMANTIC_TICACHE|Somente para uso interno.|
|SEQUENCED_OBJECT|Somente para uso interno.|
|SEQUEUE_SIZED_THREADSAFE|Somente para uso interno.|
|SESSION_KILLER|Somente para uso interno.|
|SESSION_MANAGER|Somente para uso interno.|
|SESSION_SEC_CONTEXT|Somente para uso interno.|
|SETRANGE_SYNC|Somente para uso interno.|
|SHARABLE_SESSION_OBJECTS|Somente para uso interno.|
|SLO_INFO_LIST|Somente para uso interno.|
|SNI|Somente para uso interno.|
|SNI_NODE_PENDING_IO_QUEUE|Somente para uso interno.|
|SOAPSESSIONS|Somente para uso interno.|
|SOS_ABORT_TASK|Somente para uso interno.|
|SOS_ACTIVEDESCRIPTOR|Somente para uso interno.|
|SOS_BLOCKALLOCPARTIALLIST|Somente para uso interno.|
|SOS_BLOCKDESCRIPTORBUCKET|Somente para uso interno.|
|SOS_CACHESTORE|Sincroniza o acesso a vários caches na memória do SQL Server, como o cache do plano ou o cache de tabela temporária. Uma grande contenção nesse tipo de spinlock pode significar muitas coisas diferentes, dependendo do cache específico que está em contenção. Entre em contato com [!INCLUDE[msCoName](../../includes/msconame-md.md)] serviços de suporte técnico para ajudar a solucionar esse tipo de spinlock. |
|SOS_CACHESTORE_CLOCK|Somente para uso interno.|
|SOS_CLOCKALG_INTERNODE_SYNC|Somente para uso interno.|
|SOS_DEBUG_HOOK|Somente para uso interno.|
|SOS_DESCDATABUFFERLIST|Somente para uso interno.|
|SOS_LARGEPAGE_ALLOCATOR|Somente para uso interno.|
|SOS_MINITHREAD|Somente para uso interno.|
|SOS_NODE|Somente para uso interno.|
|SOS_OBJECT_POOL|Somente para uso interno.|
|SOS_OBJECT_STORE|Somente para uso interno.|
|SOS_OOM_CHECK|Somente para uso interno.|
|SOS_PHYS_PAGE_CACHE|Somente para uso interno.|
|SOS_RESOURCE_CLERK_LIST|Somente para uso interno.|
|SOS_RINGBUFFER_RECORD|Somente para uso interno.|
|SOS_RW|Somente para uso interno.|
|SOS_SATELLITE_USER_POOL|Somente para uso interno.|
|SOS_SCHEDULER|Somente para uso interno.|
|SOS_SELIST_SIZED_SLOCK|Somente para uso interno.|
|SOS_SUSPEND_QUEUE|Somente para uso interno.|
|SOS_SYSTHREAD|Somente para uso interno.|
|SOS_SYSTHREAD_DISPATCHER|Somente para uso interno.|
|SOS_TASK|Somente para uso interno.|
|SOS_TLIST|Somente para uso interno.|
|SOS_VM_LOW|Somente para uso interno.|
|SOS_WAIT_STATS|Somente para uso interno.|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|Somente para uso interno.|
|SPIN_EVENT_MUTEX|Somente para uso interno.|
|SPL_DISPATCHER_LIST|Somente para uso interno.|
|SPL_DISPATCHER_QUEUE|Somente para uso interno.|
|SPL_NONYIELD_ANALYSIS|Somente para uso interno.|
|SPL_QUERY_STORE_CTX_INITIALIZED|Somente para uso interno.|
|SPL_QUERY_STORE_EXEC_STATS_AGG|Somente para uso interno.|
|SPL_QUERY_STORE_EXEC_STATS_READ|Somente para uso interno.|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|Somente para uso interno.|
|SPL_SOS_DISPATCHER|Somente para uso interno.|
|SPL_TDS_PKT_QUEUE|Somente para uso interno.|
|SPL_XE_BUFFER_MGR|Somente para uso interno.|
|SPL_XE_DISPATCHER_QUEUE|Somente para uso interno.|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|Somente para uso interno.|
|SPL_XE_SESSION_EVENT_MGR|Somente para uso interno.|
|SPL_XE_SESSION_MGR|Somente para uso interno.|
|SPL_XE_SESSION_TARGET_MGR|Somente para uso interno.|
|SPT_PROFILE|Somente para uso interno.|
|SQL_MGR|Somente para uso interno.|
|SQL_NORM|Somente para uso interno.|
|SQLTRACE_FILE_BUFFER|Somente para uso interno.|
|SRVPROC|Somente para uso interno.|
|STACK_HASHER|Somente para uso interno.|
|SUBLATCH|Somente para uso interno.|
|SUBPDESC|Somente para uso interno.|
|SUBPDESC_LIST|Somente para uso interno.|
|SVC_BROKER_CTRL|Somente para uso interno.|
|SVC_BROKER_DEBUG_LIST|Somente para uso interno.|
|SVC_BROKER_LIST|Somente para uso interno.|
|SVC_BROKER_OBJECT|Somente para uso interno.|
|SYNCPOINT_RESOURCE|Somente para uso interno.|
|TaskElapsedExecutionMonitor|Somente para uso interno.|
|TDS_TVP|Somente para uso interno.|
|TESTTEAM|Somente para uso interno.|
|TESTTEAMEXPONENTIAL|Somente para uso interno.|
|TESTTEAMEXPONENTIALTASTAS|Somente para uso interno.|
|TESTTEAMTASTAS|Somente para uso interno.|
|TMP_SESS_KEY|Somente para uso interno.|
|TSQL_DEBUG|Somente para uso interno.|
|TXFRM_REPL|Somente para uso interno.|
|VDI_OPERATION|Somente para uso interno.|
|WINFAB_REPORT_FAULT|Somente para uso interno.|
|WRITE_PAGE_RECORDER|Somente para uso interno.|
|X_PACKET_LIST|Somente para uso interno.|
|X_PIPE|Somente para uso interno.|
|X_PIPE_DEMAND|Somente para uso interno.|
|X_PORT|Somente para uso interno.|
|XACT_LOCK_INFO|Somente para uso interno.|
|XACT_LOCKINFO_TASK|Somente para uso interno.|
|XACT_WORKSPACE|Somente para uso interno.|
|XCB|Somente para uso interno.|
|XCB_FREE_LIST|Somente para uso interno.|
|XCB_HASH|Somente para uso interno.|
|XCHNG_TRACE|Somente para uso interno.|
|XDES|Somente para uso interno.|
|XDES_HASH|Somente para uso interno.|
|XDESMGR|Somente para uso interno.|
|XDESTABLELIST|Somente para uso interno.|
|XE_RATE_LIMITER_STRETCHDB|Somente para uso interno.|
|XE_SESSION_STORAGE|Somente para uso interno.|
|XID_ARRAY|Somente para uso interno.|
|XIO_BLOCKLIST|Somente para uso interno.|
|XIO_REQSTR|Somente para uso interno.|
|XIO_SEQNUMBUMP|Somente para uso interno.|
|XIOSTATS|Somente para uso interno.|
|XTP_RT_DATA_LIST|Somente para uso interno.|
|XTS_MGR|Somente para uso interno.|
|XVB_CSN|Somente para uso interno.|
|XVB_LIST|Somente para uso interno.|
 

  
## <a name="see-also"></a>Consulte também  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [Quando o Spinlock é uma significativa Driver de utilização da CPU no SQL Server?](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [Diagnosticar e resolver contenção de Spinlock no SQL Server](https://www.microsoft.com/download/details.aspx?id=26666)
  
  


