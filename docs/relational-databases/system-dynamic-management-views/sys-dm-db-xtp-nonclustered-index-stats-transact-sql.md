---
title: sys. dm_db_xtp_nonclustered_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_nonclustered_index_stats_TSQL
- dm_db_xtp_nonclustered_index_stats
- sys.dm_db_xtp_nonclustered_index_stats_TSQL
- sys.dm_db_xtp_nonclustered_index_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_nonclustered_index_stats
ms.assetid: d55ba31c-296c-419b-9c4b-c126e0a3d156
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c7631a10e909eb0adae9d38b89c06632e2d013c2
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442457"
---
# <a name="sysdm_db_xtp_nonclustered_index_stats-transact-sql"></a>sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  sys.dm_db_xtp_nonclustered_index_stats inclui estatísticas sobre operações em índices não clusterizados em tabelas com otimização de memória. sys.dm_db_xtp_nonclustered_index_stats contém uma linha para cada índice não clusterizado em uma tabela com otimização de memória no banco de dados atual.  
  
 As estatísticas refletidas em sys.dm_db_xtp_nonclustered_index_stats são coletadas quando a estrutura de índice na memória é criada. As estruturas de índice na memória são recriadas na reinicialização do banco de dados.  
  
 Use sys.dm_db_xtp_nonclustered_index_stats para compreender e monitorar a atividade de índice durante operações DML e quando um banco de dados é colocado online. Quando um banco de dados com uma tabela com otimização de memória é reiniciado, o índice é criado através da inserção de uma linha por vez na memória. A contagem de divisões, mesclagens e consolidação de páginas pode ajudar você a compreender o trabalho realizado para criar o índice quando um banco de dados é colocado online. Você também pode analisar essas contagens antes e depois de uma série de operações DML.  
  
 Um grande número de novas tentativas é indicativo de problemas de simultaneidade; chame o Suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Para obter mais informações sobre índices não clusterizados e com otimização de memória, [SQL Server consulte Visão geral dos elementos internos do OLTP em memória](https://t.co/T6zToWc6y6), página 17.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**int**|A ID do objeto.|  
|xtp_object_id|**bigint**|ID da tabela com otimização de memória.|  
|index_id|**int**|ID do índice.|  
|delta_pages|**bigint**|O número total de páginas delta deste índice na árvore.|  
|internal_pages|**bigint**|Para uso interno. O número total de páginas internas deste índice na árvore.|  
|leaf_pages|**bigint**|O número total de páginas de folha deste índice na árvore.|  
|outstanding_retired_nodes|**bigint**|Para uso interno. O número total de nós deste índice nas estruturas internas.|  
|page_update_count|**bigint**|Número cumulativo de operações que atualizam uma página no índice.|  
|page_update_retry_count|**bigint**|Número cumulativo de repetições de uma operação que atualiza uma página no índice.|  
|page_consolidation_count|**bigint**|Número cumulativo de consolidações de página no índice.|  
|page_consolidation_retry_count|**bigint**|Número cumulativo de repetições de operações de consolidação de página.|  
|page_split_count|**bigint**|Número cumulativo de operações de divisão de página no índice.|  
|page_split_retry_count|**bigint**|Número cumulativo de repetições de operações de divisão de página.|  
|key_split_count|**bigint**|Número cumulativo de divisões chaves no índice.|  
|key_split_retry_count|**bigint**|Número cumulativo de repetições de operações de divisões chaves.|  
|page_merge_count|**bigint**|Número cumulativo de operações de mesclagem de página no índice.|  
|page_merge_retry_count|**bigint**|Número cumulativo de repetições de operações de mesclagem de página.|  
|key_merge_count|**bigint**|Número cumulativo de operações de mesclagens chaves no índice.|  
|key_merge_retry_count|**bigint**|Número cumulativo de repetições de operações de mesclagens chaves.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
