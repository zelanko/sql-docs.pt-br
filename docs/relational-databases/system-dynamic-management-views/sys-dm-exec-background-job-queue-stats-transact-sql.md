---
title: sys.DM exec_background_job_queue_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue_stats
- sys.dm_exec_background_job_queue_stats
- dm_exec_background_job_queue_stats_TSQL
- sys.dm_exec_background_job_queue_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_background_job_queue_stats dynamic management view
ms.assetid: 27f62ab5-46c4-417e-814d-8d6437034d1c
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f586e29f3c091bda3e35a5e46aabeeb8de094aae
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecbackgroundjobqueuestats-transact-sql"></a>sys.dm_exec_background_job_queue_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha que fornece estatísticas de agregação para cada trabalho de processador de consulta enviada para execução assíncrona (em segundo plano).  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_exec_background_job_queue_stats**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**queue_max_len**|**int**|Comprimento máximo da fila.|  
|**enqueued_count**|**int**|Número de solicitações postadas à fila com êxito.|  
|**started_count**|**int**|Número de solicitações que iniciaram a execução.|  
|**ended_count**|**int**|Número de solicitações atendidas com êxito ou falha.|  
|**failed_lock_count**|**int**|Número de solicitações que falharam devido a contenção de bloqueios ou deadlock.|  
|**failed_other_count**|**int**|Número de solicitações que falharam devido a outras razões.|  
|**failed_giveup_count**|**int**|Número de solicitações que falharam porque o limite de novas tentativas foi atingido.|  
|**enqueue_failed_full_count**|**int**|Número de tentativas de enfileiramento que falharam devido a fila cheia.|  
|**enqueue_failed_duplicate_count**|**int**|Número de tentativas de enfileiramento duplicadas.|  
|**elapsed_avg_ms**|**int**|Tempo médio de solicitação decorrido, em milissegundos.|  
|**elapsed_max_ms**|**int**|Tempo decorrido da solicitação mais longa, em milissegundos.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição só retorna informações para trabalhos de estatísticas de atualizações assíncronas. Para obter mais informações sobre atualização assíncrona de estatísticas, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
## <a name="permissions"></a>Permissões  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer a permissão VIEW SERVER STATE no servidor.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Premium requer a permissão VIEW DATABASE STATE no banco de dados. Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Standard e Basic requer o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] conta de administrador.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-determining-the-percentage-of-failed-background-jobs"></a>A. Determinando a porcentagem de trabalhos em segundo plano que falharam  
 O exemplo a seguir retorna a porcentagem de trabalhos em segundo plano que falharam em todas as consultas executadas.  
  
```  
SELECT   
        CASE ended_count WHEN 0   
                THEN 'No jobs ended'   
                ELSE CAST((failed_lock_count + failed_giveup_count + failed_other_count) / CAST(ended_count AS float) * 100 AS varchar(20))   
        END AS [Percent Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
### <a name="b-determining-the-percentage-of-failed-enqueue-attempts"></a>B. Determinando a porcentagem de tentativas de enfileiramento que falharam  
 O exemplo a seguir retorna a porcentagem de tentativas de enfileiramento que falharam em todas as consultas executadas.  
  
```  
SELECT   
        CASE enqueued_count WHEN 0   
                THEN 'No jobs posted'   
                ELSE CAST((enqueue_failed_full_count + enqueue_failed_duplicate_count) / CAST(enqueued_count AS float) * 100 AS varchar(20))   
        END AS [Percent Enqueue Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico &#40; relacionadas à execução Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


