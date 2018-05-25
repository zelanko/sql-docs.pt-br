---
title: sys.DM db_session_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_session_space_usage_TSQL
- dm_db_session_space_usage
- sys.dm_db_session_space_usage
- sys.dm_db_session_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_session_space_usage dynamic management view
ms.assetid: a67a6045-8e14-460a-9fe3-912b846c08c1
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 61926a7bde695d1ca8af605373cf666653c1cee5
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbsessionspaceusage-transact-sql"></a>sys.dm_db_session_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o número de páginas alocadas e desalocadas em cada sessão para o banco de dados.  
  
> [!NOTE]  
>  Essa exibição é aplicável somente para o [banco de dados tempdb](../../relational-databases/databases/tempdb-database.md).  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_db_session_space_usage**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|ID da sessão.<br /><br /> **session_id** mapeia para **session_id** na [sys.DM exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).|  
|**database_id**|**smallint**|ID do banco de dados.|  
|**user_objects_alloc_page_count**|**bigint**|Número de páginas reservadas ou alocadas para objetos de usuário por essa sessão.|  
|**user_objects_dealloc_page_count**|**bigint**|Número de páginas desalocadas e não mais reservadas para objetos de usuário por essa sessão.|  
|**internal_objects_alloc_page_count**|**bigint**|Número de páginas reservadas ou alocadas para objetos internos por essa sessão.|  
|**internal_objects_dealloc_page_count**|**bigint**|Número de páginas desalocadas e não mais reservadas para objetos internos por essa sessão.|  
|**user_objects_deferred_dealloc_page_count**|**bigint**|Número de páginas que foram marcadas para desalocação adiada.<br /><br /> **Observação:** introduzida no service packs para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="remarks"></a>Remarks  
 As páginas IAM não estão incluídas em nenhuma contagem de alocação nem desalocação relatada por essa exibição.  
  
 Os contadores de páginas são inicializados em zero (0) no começo da sessão. Os contadores rastreiam o número total de páginas alocadas ou desalocadas para tarefas que já estão concluídas na sessão. Os contadores são atualizados somente quando a tarefa termina; eles não refletem tarefas em execução.  
  
 Uma sessão pode ter simultaneamente várias solicitações ativas. Caso seja uma consulta paralela, a solicitação poderá iniciar vários threads e tarefas.  
  
 Para obter mais informações sobre as sessões, solicitações e tarefas, consulte [sys.DM exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md), [exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)e [os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).  
  
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
 ![Junções físicas para sys.DM db_session_space_usage](../../relational-databases/system-dynamic-management-views/media/join-dm-db-session-space-usage-1.gif "físico junções para sys.DM db_session_space_usage")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_db_session_space_usage.session_id|dm_exec_sessions.session_id|Um para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  



