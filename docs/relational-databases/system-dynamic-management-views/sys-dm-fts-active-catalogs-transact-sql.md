---
title: sys.dm_fts_active_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_active_catalogs_TSQL
- dm_fts_active_catalogs
- dm_fts_active_catalogs_TSQL
- sys.dm_fts_active_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_active_catalogs dynamic management view
ms.assetid: 40ab5453-040c-4d2e-bb49-e340cf90c3ee
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 91a811fd2c868194ad0fc45d75cae7649a324672
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950993"
---
# <a name="sysdmftsactivecatalogs-transact-sql"></a>sys.dm_fts_active_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre os catálogos de texto completo que têm alguma atividade de população em andamento no servidor.  
  
> [!NOTE]
>  As colunas a seguir serão removidas em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: is_paused, previous_status, previous_status_description, row_count_in_thousands, status, status_description e worker_count. Evite usar essas colunas em novos projetos de desenvolvimento e planeje a modificação dos aplicativos que as utilizam atualmente.  
  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados que contém o catálogo de texto completo ativo.|  
|**catalog_id**|**int**|ID do catálogo de texto completo ativo.|  
|**memory_address**|**varbinary(8)**|Endereço de buffers de memória alocado para a atividade de população relacionada a este catálogo de texto completo.|  
|**name**|**nvarchar(128)**|Nome do catálogo de texto completo ativo.|  
|**is_paused**|**bit**|Indica se a população do catálogo de texto completo ativo está em pausa.|  
|**status**|**int**|Estado atual do catálogo de texto completo. Um dos seguintes:<br /><br /> 0 = Inicializando<br /><br /> 1 = Pronto<br /><br /> 2 = Pausado<br /><br /> 3 = Erro temporário<br /><br /> 4 = Remontagem necessária<br /><br /> 5 = Desligado<br /><br /> 6 = Desativado para backup<br /><br /> 7 = O backup foi feito pelo catálogo<br /><br /> 8 = O catálogo está corrompido|  
|**status_description**|**nvarchar(120)**|Descrição do estado atual do catálogo de texto completo ativo.|  
|**previous_status**|**int**|Estado anterior do catálogo de texto completo. Um dos seguintes:<br /><br /> 0 = Inicializando<br /><br /> 1 = Pronto<br /><br /> 2 = Pausado<br /><br /> 3 = Erro temporário<br /><br /> 4 = Remontagem necessária<br /><br /> 5 = Desligado<br /><br /> 6 = Desativado para backup<br /><br /> 7 = O backup foi feito pelo catálogo<br /><br /> 8 = O catálogo está corrompido|  
|**previous_status_description**|**nvarchar(120)**|Descrição do estado anterior do catálogo de texto completo ativo.|  
|**worker_count**|**int**|Número de threads atualmente em execução neste catálogo de texto completo.|  
|**active_fts_index_count**|**int**|Número de índices de texto completo que estão sendo populados.|  
|**auto_population_count**|**int**|Número de tabelas com uma população automática em andamento para este catálogo de texto completo.|  
|**manual_population_count**|**int**|Número de tabelas com população manual em andamento para este catálogo de texto completo.|  
|**full_incremental_population_count**|**int**|Número de tabelas com um população completa ou incremental em andamento para este catálogo de texto completo.|  
|**row_count_in_thousands**|**int**|Número estimado de linhas (em milhares) em todos os índices de texto completo neste catálogo de texto completo.|  
|**is_importing**|**bit**|Indica se o catálogo de texto completo está sendo importado:<br /><br /> 1 = O catálogo está sendo importado.<br /><br /> 2 = O catálogo não está sendo importado.|  
  
## <a name="remarks"></a>Comentários  
 A coluna is_importing era nova no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="permissions"></a>Permissões  

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer a permissão `VIEW DATABASE STATE` no banco de dados.   
   
## <a name="physical-joins"></a>Junções físicas  
 ![Junções significativas dessa exibição de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-active-catalogs-1.gif "junções significativas dessa exibição de gerenciamento dinâmico")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|Um para um|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|Um para um|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre os catálogos de texto completo ativos no banco de dados atual.  
  
```  
SELECT catalog.name, catalog.is_importing, catalog.auto_population_count,  
  OBJECT_NAME(population.table_id) AS table_name,  
  population.population_type_description, population.is_clustered_index_scan,  
  population.status_description, population.completion_type_description,  
  population.queued_population_type_description, population.start_time,  
  population.range_count   
FROM sys.dm_fts_active_catalogs catalog   
CROSS JOIN sys.dm_fts_index_population population   
WHERE catalog.database_id = population.database_id   
AND catalog.catalog_id = population.catalog_id   
AND catalog.database_id = (SELECT dbid FROM sys.sysdatabases WHERE name = DB_NAME());  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 
 [Pesquisa de texto completo e funções e exibições de gerenciamento dinâmico de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
