---
title: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b4d3c98f54f6f72d111f96e58e1ddafaab27e949
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782814"
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Atual retorna o nível de linha e/s, bloqueio e método de acesso para rowgroups compactados em um índice columnstore. Use **sys.dm_db_column_store_row_group_operational_stats** para rastrear o período de tempo uma consulta de usuário deve aguardar para ler ou gravar em um rowgroup compactado ou uma partição de um índice columnstore e identificar rowgroups que estão encontrando atividade de e/s significativa ou pontos de acesso.  
  
 Índices de columnstore na memória não aparecem nessa DMV.  
 
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela com índice columnstore.|  
|**index_id**|**int**|ID do índice columnstore.|  
|**partition_number**|**int**|Número de partição com base 1 no índice ou heap.|  
|**row_group_id**|**int**|ID do rowgroup no índice columnstore. Isso é exclusivo dentro de uma partição.|  
|**scan_count**|**int**|Número de exames por meio do grupo de linhas, desde a última reinicialização do SQL.|  
|**delete_buffer_scan_count**|**int**|Número de vezes que o buffer de exclusão foi usado para determinar as linhas excluídas nesse grupo de linhas. Isso inclui acessar a tabela de hash na memória e a árvore b subjacente.|  
|**index_scan_count**|**int**|Número de vezes que a partição do índice columnstore foi examinada. Isso é o mesmo para todos os rowgroups na partição.|  
|**rowgroup_lock_count**|**bigint**|Contagem cumulativa de solicitações de bloqueio para esse grupo de linhas desde a última reinicialização do SQL.|  
|**rowgroup_lock_wait_count**|**bigint**|Número cumulativo de vezes que o mecanismo de banco de dados esperou por esse bloqueio de rowgroup desde a última reinicialização do SQL.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|Número cumulativo de milissegundos que o mecanismo de banco de dados aguardado esse bloqueio do rowgroup desde a última reinicialização do SQL.|  
  
## <a name="permissions"></a>Permissões  
 Requer as seguintes permissões:  
  
-   Permissão CONTROL na tabela especificada por object_id.  
  
-   A permissão VIEW DATABASE STATE para retornar informações sobre todos os objetos de banco de dados, usando o curinga de objeto @*object_id* = NULL  
  
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
  
  

