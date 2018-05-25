---
title: sys.dm_db_fts_index_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_fts_index_physical_stats_TSQL
- dm_db_fts_index_physical_stats
- dm_db_fts_index_physical_stats_TSQL
- sys.dm_db_fts_index_physical_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_fts_index_physical_stats dynamic management view
ms.assetid: 997c3278-3630-47f6-ada3-190b6c16ce0e
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 952f07e7112b316e9109e0761deecf99f694306a
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbftsindexphysicalstats-transact-sql"></a>sys.dm_db_fts_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada índice de texto completo ou semântico em cada tabela que tenha um índice de texto completo ou semântico associado.  
  
||||  
|-|-|-|  
|**Nome da coluna**|**Tipo**|**Descrição**|  
|**object_id**|int|ID do objeto da tabela que contém o índice.|  
|**fulltext_index_page_count**|**bigint**|Tamanho lógico da extração em número de páginas de índice.|  
|**keyphrase_index_page_count**|**bigint**|Tamanho lógico da extração em número de páginas de índice.|  
|**similarity_index_page_count**|**bigint**|Tamanho lógico da extração em número de páginas de índice.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, consulte [gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre o status da indexação semântica, consulte as exibições de gerenciamento dinâmico a seguir:  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como consultar o tamanho lógico de cada índice de texto completo ou semântico em cada tabela que tenha um índice de texto completo ou semântico associado:  
  
```  
SELECT * FROM sys.dm_db_fts_index_physical_stats;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
