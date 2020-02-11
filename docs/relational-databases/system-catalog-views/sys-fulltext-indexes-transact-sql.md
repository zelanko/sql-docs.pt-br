---
title: sys. fulltext_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b240c74abde034f5008416994ca9cb497e6e64f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68133798"
---
# <a name="sysfulltext_indexes-transact-sql"></a>sys.fulltext_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha por índice de texto completo de um objeto tabular.  

|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o índice de texto completo.|  
|**unique_index_id**|**int**|ID do índice de texto não completo exclusivo correspondente, usado para relacionar o índice de texto completo às linhas.|  
|**fulltext_catalog_id**|**int**|ID do catálogo de texto completo no qual o índice de texto completo reside.|  
|**is_enabled**|**bit**|1 = O índice de texto completo está atualmente habilitado.|  
|**change_tracking_state**|**char(1)**|Estado de rastreamento de alteração.<br /><br /> M = Manual<br /><br /> A = Automático<br /><br /> O = Desligado|  
|**change_tracking_state_desc**|**nvarchar (60)**|Descrição do estado de rastreamento de alteração.<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|Último rastreamento (população) que o índice de texto completo concluiu.|  
|**crawl_type**|**char(1)**|Tipo do rastreamento atual ou do último.<br /><br /> F = Rastreamento completo<br /><br /> I = Rastreamento incremental, com base em carimbo de data/hora<br /><br /> U = Rastreio de atualização, com base em notificações<br /><br /> P = O rastreamento completo está em pausa.|  
|**crawl_type_desc**|**nvarchar (60)**|Descrição do tipo de rastreamento atual ou do último.<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|Início do rastreamento atual ou do último.<br /><br /> NULL = Nenhum.|  
|**crawl_end_date**|**datetime**|Fim do rastreamento atual ou do último.<br /><br /> NULL = Nenhum.|  
|**incremental_timestamp**|**binário (8)**|Valor do carimbo de data/hora a ser usado para o próximo rastreamento incremental.<br /><br /> NULL = Nenhum.|  
|**stoplist_id**|**int**|ID da [restoplist](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) associada a este índice de texto completo.|  
|**data_space_id**|**int**|Grupo de arquivos no qual este índice de texto completo reside.|  
|**property_list_id**|**int**|ID da lista de propriedades de pesquisa associada a este índice de texto completo. NULL indic que nenhuma lista de propriedades de pesquisa associada ao índice de texto completo. Para obter mais informações sobre essa lista de propriedades de pesquisa, use a exibição de catálogo de [&#41;registered_search_property_lists de &#40;do Transact-SQL](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) .|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa um índice de texto completo na tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks2012`. O exemplo retorna a ID do objeto da tabela, a ID da lista de propriedades de pesquisa e a ID da lista de palavras irrelevantes usadas pelo índice de texto completo.  
  
> [!NOTE]  
>  Para o exemplo de código que cria esse índice de texto completo, consulte a seção "exemplos" de [CREATE FULLTEXT index &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [sys. fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [sys. fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
