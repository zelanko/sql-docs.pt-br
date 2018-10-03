---
title: sys.dm_db_task_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_task_space_usage_TSQL
- sys.dm_db_task_space_usage_TSQL
- dm_db_task_space_usage
- sys.dm_db_task_space_usage
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_task_space_usage dynamic management view
ms.assetid: fb0c87e5-43b9-466a-a8df-11b3851dc6d0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ab12b9a0c042b96803e44c479a68a110a3c560b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806734"
---
# <a name="sysdmdbtaskspaceusage-transact-sql"></a>sys.dm_db_task_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a alocação de páginas e a atividade de desalocação por tarefa do banco de dados.  
  
> [!NOTE]  
>  Este modo de exibição é aplicável somente para o [banco de dados tempdb](../../relational-databases/databases/tempdb-database.md).  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_db_task_space_usage**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|ID da sessão.|  
|**request_id**|**int**|ID de solicitação na sessão.<br /><br /> A solicitação também é chamada de lote e contém uma ou mais consultas. Uma sessão pode ter várias solicitações ativas ao mesmo tempo. Cada consulta na solicitação poderá iniciar vários threads (tarefas), se um plano de execução paralelo for usado.|  
|**exec_context_id**|**int**|ID do contexto de execução da tarefa. Para obter mais informações, consulte [os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).|  
|**database_id**|**smallint**|ID do banco de dados.|  
|**user_objects_alloc_page_count**|**bigint**|Número de páginas reservadas ou alocadas para objetos de usuário pela tarefa.|  
|**user_objects_dealloc_page_count**|**bigint**|Número de páginas desalocadas ou não mais reservadas para objetos de usuário pela tarefa.|  
|**internal_objects_alloc_page_count**|**bigint**|Número de páginas reservadas ou alocadas para objetos internos de usuário pela tarefa.|  
|**internal_objects_dealloc_page_count**|**bigint**|Número de páginas desalocadas ou não mais reservadas para objetos internos pela tarefa.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   

## <a name="remarks"></a>Comentários  
 As páginas IAM não estão incluídas em nenhuma contagem de páginas relatada pela exibição.  
  
 Os contadores de páginas são zerados (0) ao início da solicitação. Esses valores são agregados no nível de sessão quando a solicitação é concluída. Para obter mais informações, veja [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md).  
  
 Cache de tabela de trabalho, cache de tabela temporária e operações de descarte diferido afetam o número de páginas alocadas e desalocadas em uma tarefa especificada.  
  
## <a name="user-objects"></a>Objetos do usuário  
 Os objetos a seguir são incluídos nos contadores de páginas de objeto do usuário:  
  
-   Tabelas e índices definidos pelo usuário  
  
-   Índices e tabelas do sistema  
  
-   Tabelas e índices temporários globais  
  
-   Tabelas e índices temporários locais  
  
-   Variáveis de tabela  
  
-   Tabelas retornadas nas funções com valor de tabela  
  
## <a name="internal-objects"></a>Objetos internos  
 Objetos internos estão apenas em **tempdb**. Os seguintes objetos são incluídos nos contadores de páginas de objeto de usuário:  
  
-   Tabelas de trabalho para operações de cursor ou spool e armazenamento temporário de LOB (Objeto Grande)  
  
-   Arquivos de trabalho para operações, como junção de hash  
  
-   Execuções de classificação  
  
## <a name="physical-joins"></a>Junções físicas  
 ![Junções físicas para sys.dm_db_session_task_usage](../../relational-databases/system-dynamic-management-views/media/join-dm-db-task-space-usage-1.gif "físico junções para sys.dm_db_session_task_usage")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_db_task_space_usage.request_id|dm_exec_requests.request_id|Um para um|  
|dm_db_task_space_usage.session_id|dm_exec_requests.session_id|Um para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  


