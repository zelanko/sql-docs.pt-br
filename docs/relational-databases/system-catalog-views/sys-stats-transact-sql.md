---
title: Stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.stats
- stats_TSQL
- sys.stats_TSQL
- stats
dev_langs: TSQL
helpviewer_keywords: sys.stats catalog view
ms.assetid: 42605c80-126f-460a-befb-a0b7482fae6a
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0650931e6a9c450409cd40b366a5e9fb6bf08771
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="sysstats-transact-sql"></a>sys.stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada objeto de estatística que existe para as tabelas, índices e exibições indexadas no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada índice terá uma linha de estatística correspondente com o mesmo nome e ID (**index_id** = **stats_id**), mas não cada linha de estatística tem um índice correspondente.  
  
 O modo de exibição de catálogo [stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) fornece informações de estatísticas para cada coluna no banco de dados. Para obter mais informações sobre estatísticas, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual essas estatísticas pertencem.|  
|**name**|**sysname**|Nome da estatística. É exclusiva no objeto.|  
|**stats_id**|**int**|ID da estatística. É exclusiva no objeto.<br /><br />Se as estatísticas corresponderem a um índice, o *stats_id* valor é igual a *index_id* valor o [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo.|  
|**auto_created**|**bit**|Indica se as estatísticas foram criadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = As estatísticas não foram criadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = As estatísticas foram criadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**user_created**|**bit**|Indica se as estatísticas foram criadas automaticamente por um usuário.<br /><br /> 0 = As estatísticas não foram criadas por um usuário.<br /><br /> 1 = As estatísticas foram criadas por um usuário.|  
|**no_recompute**|**bit**|Indica se as estatísticas foram criadas com o **NORECOMPUTE** opção.<br /><br /> 0 = as estatísticas não foram criadas com o **NORECOMPUTE** opção.<br /><br /> 1 = as estatísticas foram criadas com o **NORECOMPUTE** opção.|  
|**has_filter**|**bit**|0 = As estatísticas não têm um filtro e são computadas em todas as linhas.<br /><br /> 1 = As estatísticas têm um filtro e são computadas apenas em linhas que satisfazem a definição de filtro.|  
|**filter_definition são**|**nvarchar(max)**|Expressão do subconjunto de linhas incluído em estatísticas filtradas.<br /><br /> NULL = estatísticas não filtradas.|  
|**is_temporary**|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica se as estatísticas são temporárias. Estatísticas temporárias dão suporte a bancos de dados secundários de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] que são habilitados para acesso somente leitura.<br /><br /> 0 = As estatísticas não são temporárias.<br /><br /> 1 = As estatísticas são temporárias.|  
|**is_incremental**|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica se as estatísticas são criadas como estatísticas incrementais.<br /><br /> 0 = as estatísticas não são incrementais.<br /><br /> 1 = as estatísticas são incrementais.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir retornam todas as estatísticas e as colunas de estatísticas da tabela `HumanResources.Employee`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT s.name AS statistics_name  
      ,c.name AS column_name  
      ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('HumanResources.Employee');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Estatísticas](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [stats_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
 

 
