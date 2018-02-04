---
title: sys.dm_os_latch_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_latch_stats_TSQL
- dm_os_latch_stats_TSQL
- dm_os_latch_stats
- sys.dm_os_latch_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_latch_stats dynamic management view
ms.assetid: 2085d9fc-828c-453e-82ec-b54ed8347ae5
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c86a18dffb4e981145d47d5f8bc1b0a488dec52
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmoslatchstats-transact-sql"></a>sys.dm_os_latch_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações sobre todas as esperas de trava organizadas por classe.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_latch_stats**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|latch_class|**nvarchar(120)**|Nome da classe da trava.|  
|waiting_requests_count|**bigint**|Número de esperas em travas nessa classe. O contador é incrementado no início de uma espera de trava.|  
|wait_time_ms|**bigint**|Tempo de espera total, em milissegundos, nas travas dessa classe.<br /><br /> **Observação:** esta coluna é atualizada a cada cinco minutos durante uma espera de trava e no final de uma espera de trava.|  
|max_wait_time_ms|**bigint**|Tempo máximo durante qual um objeto de memória esperou essa trava. Se o valor for exageradamente alto, pode indicar um deadlock interno.|  
|pdw_node_id|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta.    
  
## <a name="remarks"></a>Remarks  
 sys.dm_os_latch_stats pode ser usado para identificar a origem de uma contenção de travamento, examinando os números e os tempos de espera relativos para as diferentes classes de trava. Em algumas situações, talvez seja possível resolver ou reduzir contenção de trava. Entretanto, pode haver situações em que seja necessário contatar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Serviço de Atendimento ao Cliente.  
  
 É possível redefinir o conteúdo de sys.dm_os_latch_stats usando `DBCC SQLPERF` da seguinte maneira:  
  
```  
DBCC SQLPERF ('sys.dm_os_latch_stats', CLEAR);  
GO  
```  
  
 Isso redefine todos os contadores como 0.  
  
> [!NOTE]  
>  Essas estatísticas não persistirão se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reiniciado. Todos os dados são acumulados desde a última vez em que as estatísticas foram redefinidas ou desde que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado.  
  
## <a name="latches"></a>Travas  
 Uma trava é um objeto de sincronização leve usado por vários componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A trava é usada basicamente para sincronizar páginas de banco de dados. Cada trava é associada a uma única unidade de alocação.  
  
 Uma espera de trava ocorre quando uma solicitação de trava não pode ser concedida imediatamente, porque a trava foi retida por outro thread em um modo conflitante. Ao contrário dos bloqueios, a trava é liberada logo após a operação, mesmo em operações de gravação.  
  
 As travas são agrupadas em classes baseadas em componentes e em utilização. Zero ou mais travas de uma classe específica podem existir a qualquer momento em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  sys.dm_os_latch_stats não localiza as solicitações de trava que foram concedidas imediatamente ou que falharam sem esperar.  
  
 A tabela a seguir contém breves descrições das diversas classes de trava.  
  
|Classe de trava|Description|  
|-----------------|-----------------|  
|ALLOC_CREATE_RINGBUF|Usada internamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para inicializar a sincronização da criação de um buffer de anel de alocação.|  
|ALLOC_CREATE_FREESPACE_CACHE|Usada para inicializar a sincronização de caches internos de espaço livre para heaps.|  
|ALLOC_CACHE_MANAGER|Usada para sincronizar testes de coerência internos.|  
|ALLOC_FREESPACE_CACHE|Usada para sincronizar o acesso a um cache de páginas com espaço disponível para heaps e BLOBs (objetos binários grandes). A contenção em travas dessa classe pode ocorrer quando várias conexões tentam inserir linhas em um heap ou BLOB ao mesmo tempo. É possível reduzir essa contenção através do particionamento do objeto. Cada partição possui sua própria trava. O particionamento distribui as inserções em várias travas.|  
|ALLOC_EXTENT_CACHE|Usada para sincronizar o acesso a um cache de extensões contendo páginas que não são alocadas. A contenção em travas dessa classe pode ocorrer quando várias conexões tentam alocar páginas de dados na mesma unidade de alocação ao mesmo tempo. Essa contenção pode ser reduzida através do particionamento do objeto do qual a unidade de alocação faz parte.|  
|ACCESS_METHODS_DATASET_PARENT|Usada para sincronizar o acesso de conjunto de dados filho ao conjunto de dados pai durante operações paralelas.|  
|ACCESS_METHODS_HOBT_FACTORY|Usada para sincronizar o acesso a uma tabela de hash interna.|  
|ACCESS_METHODS_HOBT|Usada para sincronizar o acesso à representação em memória de um HoBt.|  
|ACCESS_METHODS_HOBT_COUNT|Usada para sincronizar o acesso a uma página HoBt e contadores de linha.|  
|ACCESS_METHODS_HOBT_VIRTUAL_ ROOT|Usada para sincronizar o acesso à abstração de página raiz de uma árvore B interna.|  
|ACCESS_METHODS_CACHE_ONLY_ HOBT_ALLOC|Usada para sincronizar o acesso de tabela de trabalho.|  
|ACCESS_METHODS_BULK_ALLOC|Usada para sincronizar o acesso dentro de alocadores em massa.|  
|ACCESS_METHODS_SCAN_RANGE_ GENERATOR|Usada para sincronizar o acesso a um gerador de intervalos durante exames paralelos.|  
|ACCESS_METHODS_KEY_RANGE_ GENERATOR|Usada para sincronizar o acesso a operações read-ahead durante exames paralelos de intervalo de chave.|  
|APPEND_ONLY_STORAGE_INSERT_ POINT|Usada para sincronizar inserções em unidades de armazenamento rápidas somente de acréscimo.|  
|APPEND_ONLY_STORAGE_FIRST_ALLOC|Usada ao sincronizar a primeira alocação para uma unidade de armazenamento somente de acréscimo.|  
|APPEND_ONLY_STORAGE_UNIT_ MANAGER|Usada para sincronização de acesso de estrutura de dados interna dentro do gerenciador de unidades de armazenamento rápidas somente de acréscimo.|  
|APPEND_ONLY_STORAGE_MANAGER|Usada para sincronizar operações de redução no gerenciador de unidades de armazenamento rápidas somente de acréscimo.|  
|BACKUP_RESULT_SET|Usada para sincronizar conjuntos de resultados de backup paralelos.|  
|BACKUP_TAPE_POOL|Usada para sincronizar pools de fita de backup.|  
|BACKUP_LOG_REDO|Usada para sincronizar operações que refazem o log de backup.|  
|BACKUP_INSTANCE_ID|Usada para sincronizar a geração de IDs de instâncias para contadores de monitoramento de desempenho de backup.|  
|BACKUP_MANAGER|Usada para sincronizar o gerenciador de backup interno.|  
|BACKUP_MANAGER_DIFFERENTIAL|Usada para sincronizar operações de backup diferencial com DBCC.|  
|BACKUP_OPERATION|Usada para a sincronização da estrutura de dados interna dentro de uma operação de backup, tal como banco de dados, log ou backup de arquivo.|  
|BACKUP_FILE_HANDLE|Usada para sincronizar operações de abertura de arquivos durante uma operação de restauração.|  
|BUFFER|Usada para sincronizar o acesso a curto prazo a páginas de banco de dados. Uma trava de buffer é necessária antes de ler ou modificar qualquer página de banco de dados. A contenção da trava de buffer pode indicar vários problemas, inclusive hotpages e E/S lentas.<br /><br /> Essa classe de trava abrange todos os possíveis usos de travas de página. sys.DM os_wait_stats faz a diferença entre as esperas de trava de página causadas pelas operações de e/s e de leitura e gravação na página.|  
|BUFFER_POOL_GROW|Usada para a sincronização do gerenciador de buffer interno durante as operações de geração de pools de buffers.|  
|DATABASE_CHECKPOINT|Usada para serializar pontos de verificação dentro de um banco de dados.|  
|CLR_PROCEDURE_HASHTABLE|Somente para uso interno.|  
|CLR_UDX_STORE|Somente para uso interno.|  
|CLR_DATAT_ACCESS|Somente para uso interno.|  
|CLR_XVAR_PROXY_LIST|Somente para uso interno.|  
|DBCC_CHECK_AGGREGATE|Somente para uso interno.|  
|DBCC_CHECK_RESULTSET|Somente para uso interno.|  
|DBCC_CHECK_TABLE|Somente para uso interno.|  
|DBCC_CHECK_TABLE_INIT|Somente para uso interno.|  
|DBCC_CHECK_TRACE_LIST|Somente para uso interno.|  
|DBCC_FILE_CHECK_OBJECT|Somente para uso interno.|  
|DBCC_PERF|Usada para sincronizar contadores de monitor de desempenho internos.|  
|DBCC_PFS_STATUS|Somente para uso interno.|  
|DBCC_OBJECT_METADATA|Somente para uso interno.|  
|DBCC_HASH_DLL|Somente para uso interno.|  
|EVENTING_CACHE|Somente para uso interno.|  
|FCB|Usada para sincronizar o acesso ao bloco de controle de arquivo.|  
|FCB_REPLICA|Somente para uso interno.|  
|FGCB_ALLOC|Use para sincronizar o acesso às informações de alocação round robin em um grupo de arquivos.|  
|FGCB_ADD_REMOVE|Use para sincronizar o acesso a grupos de arquivos para as operações de arquivo ADD e DROP.|  
|FILEGROUP_MANAGER|Somente para uso interno.|  
|FILE_MANAGER|Somente para uso interno.|  
|FILESTREAM_FCB|Somente para uso interno.|  
|FILESTREAM_FILE_MANAGER|Somente para uso interno.|  
|FILESTREAM_GHOST_FILES|Somente para uso interno.|  
|FILESTREAM_DFS_ROOT|Somente para uso interno.|  
|LOG_MANAGER|Somente para uso interno.|  
|FULLTEXT_DOCUMENT_ID|Somente para uso interno.|  
|FULLTEXT_DOCUMENT_ID_ TRANSACTION|Somente para uso interno.|  
|FULLTEXT_DOCUMENT_ID_NOTIFY|Somente para uso interno.|  
|FULLTEXT_LOGS|Somente para uso interno.|  
|FULLTEXT_CRAWL_LOG|Somente para uso interno.|  
|FULLTEXT_ADMIN|Somente para uso interno.|  
|FULLTEXT_AMDIN_COMMAND_CACHE|Somente para uso interno.|  
|FULLTEXT_LANGUAGE_TABLE|Somente para uso interno.|  
|FULLTEXT_CRAWL_DM_LIST|Somente para uso interno.|  
|FULLTEXT_CRAWL_CATALOG|Somente para uso interno.|  
|FULLTEXT_FILE_MANAGER|Somente para uso interno.|  
|DATABASE_MIRRORING_REDO|Somente para uso interno.|  
|DATABASE_MIRRORING_SERVER|Somente para uso interno.|  
|DATABASE_MIRRORING_CONNECTION|Somente para uso interno.|  
|DATABASE_MIRRORING_STREAM|Somente para uso interno.|  
|QUERY_OPTIMIZER_VD_MANAGER|Somente para uso interno.|  
|QUERY_OPTIMIZER_ID_MANAGER|Somente para uso interno.|  
|QUERY_OPTIMIZER_VIEW_REP|Somente para uso interno.|  
|RECOVERY_BAD_PAGE_TABLE|Somente para uso interno.|  
|RECOVERY_MANAGER|Somente para uso interno.|  
|SECURITY_OPERATION_RULE_TABLE|Somente para uso interno.|  
|SECURITY_OBJPERM_CACHE|Somente para uso interno.|  
|SECURITY_CRYPTO|Somente para uso interno.|  
|SECURITY_KEY_RING|Somente para uso interno.|  
|SECURITY_KEY_LIST|Somente para uso interno.|  
|SERVICE_BROKER_CONNECTION_RECEIVE|Somente para uso interno.|  
|SERVICE_BROKER_TRANSMISSION|Somente para uso interno.|  
|SERVICE_BROKER_TRANSMISSION_UPDATE|Somente para uso interno.|  
|SERVICE_BROKER_TRANSMISSION_STATE|Somente para uso interno.|  
|SERVICE_BROKER_TRANSMISSION_ERRORS|Somente para uso interno.|  
|SSBXmitWork|Somente para uso interno.|  
|SERVICE_BROKER_MESSAGE_TRANSMISSION|Somente para uso interno.|  
|SERVICE_BROKER_MAP_MANAGER|Somente para uso interno.|  
|SERVICE_BROKER_HOST_NAME|Somente para uso interno.|  
|SERVICE_BROKER_READ_CACHE|Somente para uso interno.|  
|SERVICE_BROKER_WAITFOR_MANAGER| Usado para sincronizar um mapa de nível de instância de filas de serviço. Existe uma fila por tupla de ID, versão do banco de dados e ID de fila do banco de dados. A contenção em travas dessa classe pode ocorrer quando o número de conexões é: em um WAITFOR(RECEIVE) espera estado. chamando WAITFOR(RECEIVE); excedendo o tempo limite de WAITFOR; recebendo uma mensagem. Confirmar ou reverter a transação que contém o WAITFOR(RECEIVE); Você pode reduzir a contenção, reduzindo o número de threads em um estado de espera WAITFOR(RECEIVE). |  
|SERVICE_BROKER_WAITFOR_TRANSACTION_DATA|Somente para uso interno.|  
|SERVICE_BROKER_TRANSMISSION_TRANSACTION_DATA|Somente para uso interno.|  
|SERVICE_BROKER_TRANSPORT|Somente para uso interno.|  
|SERVICE_BROKER_MIRROR_ROUTE|Somente para uso interno.|  
|TRACE_ID|Somente para uso interno.|  
|TRACE_AUDIT_ID|Somente para uso interno.|  
|TRACE|Somente para uso interno.|  
|TRACE_CONTROLLER|Somente para uso interno.|  
|TRACE_EVENT_QUEUE|Somente para uso interno.|  
|TRANSACTION_DISTRIBUTED_MARK|Somente para uso interno.|  
|TRANSACTION_OUTCOME|Somente para uso interno.|  
|NESTING_TRANSACTION_READONLY|Somente para uso interno.|  
|NESTING_TRANSACTION_FULL|Somente para uso interno.|  
|MSQL_TRANSACTION_MANAGER|Somente para uso interno.|  
|DATABASE_AUTONAME_MANAGER|Somente para uso interno.|  
|UTILITY_DYNAMIC_VECTOR|Somente para uso interno.|  
|UTILITY_SPARSE_BITMAP|Somente para uso interno.|  
|UTILITY_DATABASE_DROP|Somente para uso interno.|  
|UTILITY_DYNAMIC_MANAGER_VIEW|Somente para uso interno.|  
|UTILITY_DEBUG_FILESTREAM|Somente para uso interno.|  
|UTILITY_LOCK_INFORMATION|Somente para uso interno.|  
|VERSIONING_TRANSACTION|Somente para uso interno.|  
|VERSIONING_TRANSACTION_LIST|Somente para uso interno.|  
|VERSIONING_TRANSACTION_CHAIN|Somente para uso interno.|  
|VERSIONING_STATE|Somente para uso interno.|  
|VERSIONING_STATE_CHANGE|Somente para uso interno.|  
|KTM_VIRTUAL_CLOCK|Somente para uso interno.|  
  
## <a name="see-also"></a>Consulte também  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


