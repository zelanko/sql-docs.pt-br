---
title: sys.stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.stats
- stats_TSQL
- sys.stats_TSQL
- stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats catalog view
ms.assetid: 42605c80-126f-460a-befb-a0b7482fae6a
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d81d0447558f964839b8849fe141f127fe1e37c
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982142"
---
# <a name="sysstats-transact-sql"></a>sys.stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada objeto de estatística que existe para as tabelas, índices e exibições indexadas no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada índice terá uma linha de estatísticas correspondente com o mesmo nome e ID (**index_id** = **stats_id**), mas nem todas as linhas de estatísticas têm um índice correspondente.  
  
 A exibição de catálogo [Sys. stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) fornece informações de estatísticas para cada coluna no banco de dados. Para obter mais informações sobre estatísticas, consulte [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual essas estatísticas pertencem.|  
|**name**|**sysname**|Nome da estatística. É exclusiva no objeto.|  
|**stats_id**|**int**|ID da estatística. É exclusiva no objeto.<br /><br />Se as estatísticas corresponderem a um índice, o valor de *stats_id* será o mesmo que o valor de *index_id* na exibição de catálogo [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) .|  
|**auto_created**|**bit**|Indica se as estatísticas foram criadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = As estatísticas não foram criadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = As estatísticas foram criadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**user_created**|**bit**|Indica se as estatísticas foram criadas automaticamente por um usuário.<br /><br /> 0 = As estatísticas não foram criadas por um usuário.<br /><br /> 1 = As estatísticas foram criadas por um usuário.|  
|**no_recompute**|**bit**|Indica se as estatísticas foram criadas com a opção **NORECOMPUTE** .<br /><br /> 0 = as estatísticas não foram criadas com a opção **NORECOMPUTE** .<br /><br /> 1 = as estatísticas foram criadas com a opção **NORECOMPUTE** .|  
|**has_filter**|**bit**|0 = As estatísticas não têm um filtro e são computadas em todas as linhas.<br /><br /> 1 = As estatísticas têm um filtro e são computadas apenas em linhas que satisfazem a definição de filtro.|  
|**filter_definition**|**nvarchar(max)**|Expressão do subconjunto de linhas incluído em estatísticas filtradas.<br /><br /> NULL = estatísticas não filtradas.|  
|**is_temporary**|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Indica se as estatísticas são temporárias. Estatísticas temporárias dão suporte a bancos de dados secundários de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] que são habilitados para acesso somente leitura.<br /><br /> 0 = As estatísticas não são temporárias.<br /><br /> 1 = As estatísticas são temporárias.|  
|**is_incremental**|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Indica se as estatísticas são criadas como estatísticas incrementais.<br /><br /> 0 = as estatísticas não são incrementais.<br /><br /> 1 = as estatísticas são incrementais.|  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Estatística](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
 

 
