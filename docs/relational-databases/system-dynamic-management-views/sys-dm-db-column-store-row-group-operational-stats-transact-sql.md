---
title: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: db5154b1b99b548a0757b83c3f79c39c23b777e3
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna atual e/s, bloqueio, de nível de linha e método de acesso para rowgroups compactados em um índice columnstore. Use **sys.dm_db_column_store_row_group_operational_stats** para rastrear o período de tempo de uma consulta de usuário deve aguardar para ler ou gravar em um grupo de linhas compactado ou uma partição de um índice columnstore e identificar rowgroups que estão encontrando atividade de e/s significativa ou pontos de acesso.  
  
 Índices columnstore na memória não aparecem nessa DMV.  
 
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|ID da tabela com índice columnstore.|  
|**index_id**|**Int**|ID do índice columnstore.|  
|**partition_number**|**Int**|Número de partição com base 1 no índice ou heap.|  
|**row_group_id**|**Int**|ID do grupo de linhas no índice columnstore. Isso é exclusivo dentro de uma partição.|  
|**scan_count**|**Int**|Número de exames por meio do grupo de linhas, desde a última reinicialização do SQL.|  
|**delete_buffer_scan_count**|**Int**|Número de vezes que o buffer de exclusão foi usado para determinar as linhas excluídas neste grupo de linhas. Isso inclui acesso a tabela de hash na memória e a árvore b subjacente.|  
|**index_scan_count**|**Int**|Número de vezes que a partição do índice columnstore foi examinada. Isso é o mesmo para todos os rowgroups na partição.|  
|**rowgroup_lock_count**|**bigint**|Contagem cumulativa de solicitações de bloqueio para este grupo de linhas desde a última reinicialização do SQL.|  
|**rowgroup_lock_wait_count**|**bigint**|Número cumulativo de vezes que o mecanismo de banco de dados aguardou esse bloqueio do rowgroup desde a última reinicialização do SQL.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|Número cumulativo de milissegundos que o mecanismo de banco de dados aguardou esse bloqueio do rowgroup desde a última reinicialização do SQL.|  
  
## <a name="permissions"></a>Permissões  
 Requer as seguintes permissões:  
  
-   Permissão CONTROL na tabela especificada pelo object_id.  
  
-   Permissão VIEW DATABASE STATE para retornar informações sobre todos os objetos no banco de dados, usando o curinga de objeto @*object_id* = NULL  
  
 Conceder VIEW DATABASE STATE permite que todos os objetos no banco de dados sejam retornados, independentemente de qualquer permissão CONTROL negada a objetos específicos.  
  
 Negar VIEW DATABASE STATE impede que todos os objetos do banco de dados sejam retornados, independentemente de qualquer permissão CONTROL concedida a objetos específicos. Além disso, quando o curinga de banco de dados @*database_id*= NULL for especificado, o banco de dados é omitido.  
  
 Para obter mais informações, consulte [funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições e funções de gerenciamento dinâmico relacionadas ao índice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

