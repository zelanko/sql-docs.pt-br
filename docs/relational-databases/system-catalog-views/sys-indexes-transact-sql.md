---
title: sys.indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ff8fb876ace87e26522cc19ffdc97359a9216844
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387975"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha por índice ou heap de um objeto tabular, como uma tabela, exibição ou função com valor de tabela.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual este índice pertence.|  
|**name**|**sysname**|Nome do índice. **nome** só é exclusivo dentro do objeto.<br /><br /> NULL = Heap|  
|**index_id**|**int**|ID do índice. **index_id** é exclusivo somente dentro do objeto.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> > 1 = índice não clusterizado|  
|**type**|**tinyint**|Tipo de índice:<br /><br /> 0 = Heap<br /><br /> 1 = Clusterizado<br /><br /> 2 = Não clusterizado<br /><br /> 3 = XML<br /><br /> 4 = Espacial<br /><br /> 5 = índice columnstore clusterizado. **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 6 = índice columnstore não clusterizado. **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 7 = índice nonclustered hash. **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**type_desc**|**nvarchar(60)**|Descrição de tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> COLUMNSTORE CLUSTERIZADO - **aplica-se ao**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> COLUMNSTORE não CLUSTERIZADO - **aplica-se ao**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> HASH NÃO CLUSTERIZADOS: Os índices NONCLUSTERED HASH têm suporte apenas em tabelas com otimização de memória. A exibição sys.hash_indexes mostra os índices de hash atuais e as propriedades de hash. Para obter mais informações, consulte [hash_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md). **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**is_unique**|**bit**|1 = O índice é exclusivo.<br /><br /> 0 = O índice não é exclusivo.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**data_space_id**|**int**|A ID do espaço de dados deste índice. O espaço de dados é um grupo de arquivos ou um esquema de partição.<br /><br /> 0 = **object_id** é uma função com valor de tabela ou índice na memória.|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY está ON.<br /><br /> 0 = IGNORE_DUP_KEY está OFF.|  
|**is_primary_key**|**bit**|1 = O índice faz parte de uma restrição PRIMARY KEY.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_unique_constraint**|**bit**|1 = O índice faz parte de uma restrição UNIQUE.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**fill_factor**|**tinyint**|> 0 = porcentagem de FILLFACTOR usada quando o índice foi criado ou reconstruído.<br /><br /> 0 = Valor padrão<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_padded**|**bit**|1 = PADINDEX está ON.<br /><br /> 0 = PADINDEX está OFF.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_disabled**|**bit**|1 = O índice está desabilitado.<br /><br /> 0 = O índice não está desabilitado.|  
|**is_hypothetical**|**bit**|1 = O índice é hipotético e não pode ser usado diretamente como um caminho de acesso a dados. Índices hipotéticos mantêm estatísticas em nível de coluna.<br /><br /> 0 = O índice não é hipotético.|  
|**allow_row_locks**|**bit**|1 = O índice permite bloqueios de linha.<br /><br /> 0 = O índice não permite bloqueios de linha.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**allow_page_locks**|**bit**|1 = O índice permite bloqueios de página.<br /><br /> 0 = O índice não permite bloqueios de página.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**has_filter**|**bit**|1 = O índice tem um filtro e só contém linhas que atendem à definição do filtro.<br /><br /> 0 = O índice não tem um filtro.|  
|**filter_definition**|**nvarchar(max)**|Expressão do subconjunto de linhas incluído no índice filtrado.<br /><br /> NULL para índice heap ou não filtrado.|  
|**auto_created**|**bit**|1 = o índice foi criado pelo ajuste automático.<br /><br />0 = índice foi criado pelo usuário.
|**optimize_for_sequential_key**|**bit**|1 = o índice tem otimização de inserção de última página habilitada.<br><br>0 = valor padrão. Índice tem otimização de inserção de última página desabilitada.|

  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os índices da tabela `Production.Product` no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.  
  
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
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
