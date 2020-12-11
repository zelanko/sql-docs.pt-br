---
description: sys.dm_exec_background_job_queue (Transact-SQL)
title: sys.dm_exec_background_job_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b60bed7d0e0126b8ac765c2fc910d75da6475a01
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97334562"
---
# <a name="sysdm_exec_background_job_queue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada trabalho de processador de consulta agendado para execução assíncrona (em segundo plano).  
  
> **OBSERVAÇÃO!** Para chamá-lo de **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** ou **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** , use o nome **Sys.dm_pdw_nodes_exec_background_job_queue**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|Hora em que a tarefa foi adicionada à fila.|  
|**job_id**|**int**|Job identifier.|  
|**database_id**|**int**|Banco de dados no qual a tarefa será executada.|  
|**object_id1**|**int**|O valor depende do tipo de trabalho. Para obter mais informações, consulte a seção Comentários.|  
|**object_id2**|**int**|O valor depende do tipo de trabalho. Para obter mais informações, consulte a seção Comentários.|  
|**object_id3**|**int**|O valor depende do tipo de trabalho. Para obter mais informações, consulte a seção Comentários.|  
|**object_id4**|**int**|O valor depende do tipo de trabalho. Para obter mais informações, consulte a seção Comentários.|  
|**error_code**|**int**|Código de erro se o trabalho for reinserido devido à falha. NULL se suspenso, não coletado ou concluído.|  
|**request_type**|**smallint**|Tipo de solicitação de trabalho.|  
|**retry_count**|**smallint**|Número de vezes que o trabalho foi coletado da fila e reinserido devido à falta de recursos ou outros motivos.|  
|**in_progress**|**smallint**|Indica se o trabalho iniciou a execução.<br /><br /> 1 = Iniciado<br /><br /> 0 = Ainda esperando|  
|**session_id**|**smallint**|Identificador de sessão.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
  
## <a name="remarks"></a>Comentários  
 Esta exibição só retorna informações para trabalhos de estatísticas de atualizações assíncronas. Para obter mais informações sobre estatísticas de atualização assíncronas, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
 Os valores de **object_id1** por meio de **object_id4** dependem do tipo de solicitação de trabalho. A tabela a seguir resume o significado dessas colunas para os diferentes tipos de trabalho.  
  
|Tipo de solicitação|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|Estatísticas de atualização assíncrona|Tabela ou ID de exibição|ID de estatísticas|Não usado|Não usado|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o número de trabalhos assíncronos ativos na fila em segundo plano para cada banco de dados na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Estatística](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



