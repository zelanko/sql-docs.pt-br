---
title: sys.DM os_memory_cache_hash_tables (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
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
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 887ff777b24fd130692368352e05396659a60b12
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosmemorycachehashtables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada cache ativo na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_memory_cache_hash_tables**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|Endereço (chave primária) da entrada de cache. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Nome do cache. Não permite valor nulo.|  
|**tipo**|**nvarchar (60)**|Tipo de cache. Não permite valor nulo.|  
|**table_level**|**int**|Número da tabela hash. Um cache específico pode ter várias tabelas hash que correspondem a funções hash diferentes. Não permite valor nulo.|  
|**buckets_count**|**int**|Número de partições de memória na tabela hash. Não permite valor nulo.|  
|**buckets_in_use_count**|**int**|Número de partições de memória que estão sendo usadas atualmente. Não permite valor nulo.|  
|**buckets_min_length**|**int**|Número mínimo de entradas de cache em uma partição de memória. Não permite valor nulo.|  
|**buckets_max_length**|**int**|Número máximo de entradas de cache em uma partição de memória. Não permite valor nulo.|  
|**buckets_avg_length**|**int**|Número médio de entradas de cache em cada partição de memória. Não permite valor nulo.|  
|**buckets_max_length_ever**|**int**|Número máximo de entradas em cache em uma partição de memória hash para esta tabela hash, desde que o servidor foi iniciado. Não permite valor nulo.|  
|**hits_count**|**bigint**|Número de acertos do cache. Não permite valor nulo.|  
|**misses_count**|**bigint**|Número de ausências de cache. Não permite valor nulo.|  
|**buckets_avg_scan_hit_length**|**int**|Número médio de entradas examinadas em uma partição de memória antes de um item pesquisado ser localizado. Não permite valor nulo.|  
|**buckets_avg_scan_miss_length**|**int**|Número médio de entradas examinadas em uma partição de memória antes do encerramento sem-êxito da pesquisa. Não permite valor nulo.|  
|**pdw_node_id**|**int**|O identificador para o nó que essa distribuição é no.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta.  
  
## <a name="see-also"></a>Consulte também  
 
  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


