---
title: sys. Indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.indexes
- indexes
- sys.indexes_TSQL
- indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes catalog view
ms.assetid: 066bd9ac-6554-4297-88fe-d740de1f94a8
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1a83f1addba51d14ced6d38aa18b5c5f2d1d9082
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33182452"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha por índice ou heap de um objeto tabular, como uma tabela, exibição ou função com valor de tabela.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|ID do objeto ao qual este índice pertence.|  
|**name**|**sysname**|Nome do índice. **nome** só é exclusivo dentro do objeto.<br /><br /> NULL = Heap|  
|**index_id**|**Int**|ID do índice. **index_id** só é exclusivo dentro do objeto.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> > 1 = Índice não clusterizado|  
|**type**|**tinyint**|Tipo de índice:<br /><br /> 0 = Heap<br /><br /> 1 = Clusterizado<br /><br /> 2 = Não clusterizado<br /><br /> 3 = XML<br /><br /> 4 = Espacial<br /><br /> 5 = índice columnstore clusterizado. **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 6 = índice columnstore não clusterizado. **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 7 = índice de hash não clusterizados. **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**type_desc**|**nvarchar(60)**|Descrição de tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> COLUMNSTORE CLUSTERIZADO - **aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Não CLUSTERIZADO COLUMNSTORE - **aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> NONCLUSTERED HASH: Os índices NONCLUSTERED HASH têm suporte apenas em tabelas com otimização de memória. A exibição sys.hash_indexes mostra os índices de hash atuais e as propriedades de hash. Para obter mais informações, consulte [sys. hash_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md). **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**is_unique**|**bit**|1 = O índice é exclusivo.<br /><br /> 0 = O índice não é exclusivo.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**data_space_id**|**Int**|A ID do espaço de dados deste índice. O espaço de dados é um grupo de arquivos ou um esquema de partição.<br /><br /> 0 = **object_id** é uma função com valor de tabela ou índice na memória.|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY está ON.<br /><br /> 0 = IGNORE_DUP_KEY está OFF.|  
|**is_primary_key**|**bit**|1 = O índice faz parte de uma restrição PRIMARY KEY.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_unique_constraint**|**bit**|1 = O índice faz parte de uma restrição UNIQUE.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**fill_factor**|**tinyint**|>0 = Porcentagem de FILLFACTOR usada quando o índice foi criado ou reconstruído.<br /><br /> 0 = Valor padrão<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_padded**|**bit**|1 = PADINDEX está ON.<br /><br /> 0 = PADINDEX está OFF.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_disabled**|**bit**|1 = O índice está desabilitado.<br /><br /> 0 = O índice não está desabilitado.|  
|**is_hypothetical**|**bit**|1 = O índice é hipotético e não pode ser usado diretamente como um caminho de acesso a dados. Índices hipotéticos mantêm estatísticas em nível de coluna.<br /><br /> 0 = O índice não é hipotético.|  
|**allow_row_locks**|**bit**|1 = O índice permite bloqueios de linha.<br /><br /> 0 = O índice não permite bloqueios de linha.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**allow_page_locks**|**bit**|1 = O índice permite bloqueios de página.<br /><br /> 0 = O índice não permite bloqueios de página.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**has_filter**|**bit**|1 = O índice tem um filtro e só contém linhas que atendem à definição do filtro.<br /><br /> 0 = O índice não tem um filtro.|  
|**filter_definition são**|**nvarchar(max)**|Expressão do subconjunto de linhas incluído no índice filtrado.<br /><br /> NULL para índice heap ou não filtrado.|  
|**auto_created**|**bit**|1 = índice foi criado, o ajuste automático.<br /><br />0 = índice foi criado pelo usuário.
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os índices da tabela `Production.Product` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('Production.Product');  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP na memória &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
