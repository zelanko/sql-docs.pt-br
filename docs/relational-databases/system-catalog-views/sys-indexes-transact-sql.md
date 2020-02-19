---
title: sys. Indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2020
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3208f538a1c1e111913c0808a8213743fed41bcc
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2020
ms.locfileid: "77179287"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha por índice ou heap de um objeto tabular, como uma tabela, exibição ou função com valor de tabela.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual este índice pertence.|  
|**name**|**sysname**|Nome do índice. o **nome** é exclusivo somente dentro do objeto.<br /><br /> NULL = Heap|  
|**index_id**|**int**|ID do índice. **index_id** é exclusivo somente dentro do objeto.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> >1 = Índice não clusterizado|  
|**tipo**|**tinyint**|Tipo de índice:<br /><br /> 0 = Heap<br /><br /> 1 = Clusterizado<br /><br /> 2 = Não clusterizado<br /><br /> 3 = XML<br /><br /> 4 = Espacial<br /><br /> 5 = índice columnstore clusterizado. **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> 6 = índice columnstore não clusterizado. **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> 7 = índice de hash não clusterizado. **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.|  
|**type_desc**|**nvarchar (60)**|Descrição de tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> COLUMNSTORE clusterizado – **aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> COLUMNSTORE não clusterizado – **aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> HASH não CLUSTERIZAdo: há suporte para índices de HASH não CLUSTERIZAdos somente em tabelas com otimização de memória. A exibição sys.hash_indexes mostra os índices de hash atuais e as propriedades de hash. Para obter mais informações, consulte [Sys. hash_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md). **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.|  
|**is_unique**|**bit**|1 = O índice é exclusivo.<br /><br /> 0 = O índice não é exclusivo.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**data_space_id**|**int**|A ID do espaço de dados deste índice. O espaço de dados é um grupo de arquivos ou um esquema de partição.<br /><br /> 0 = **object_id** é uma função com valor de tabela ou índice na memória.|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY está ON.<br /><br /> 0 = IGNORE_DUP_KEY está OFF.|  
|**is_primary_key**|**bit**|1 = O índice faz parte de uma restrição PRIMARY KEY.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_unique_constraint**|**bit**|1 = O índice faz parte de uma restrição UNIQUE.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**fill_factor**|**tinyint**|> 0 = porcentagem FILLFACTOR usada quando o índice foi criado ou recriado.<br /><br /> 0 = Valor padrão<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_padded**|**bit**|1 = PADINDEX está ON.<br /><br /> 0 = PADINDEX está OFF.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**is_disabled**|**bit**|1 = O índice está desabilitado.<br /><br /> 0 = O índice não está desabilitado.|  
|**is_hypothetical**|**bit**|1 = O índice é hipotético e não pode ser usado diretamente como um caminho de acesso a dados. Índices hipotéticos mantêm estatísticas em nível de coluna.<br /><br /> 0 = O índice não é hipotético.|  
|**allow_row_locks**|**bit**|1 = O índice permite bloqueios de linha.<br /><br /> 0 = O índice não permite bloqueios de linha.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**allow_page_locks**|**bit**|1 = O índice permite bloqueios de página.<br /><br /> 0 = O índice não permite bloqueios de página.<br /><br /> Sempre 0 para índices columnstore clusterizados.|  
|**has_filter**|**bit**|1 = O índice tem um filtro e só contém linhas que atendem à definição do filtro.<br /><br /> 0 = O índice não tem um filtro.|  
|**filter_definition**|**nvarchar(max)**|Expressão do subconjunto de linhas incluído no índice filtrado.<br /><br /> NULL para heap, índice não filtrado ou permissões insuficientes na tabela.|  
|**auto_created**|**bit**|1 = o índice foi criado pelo ajuste automático.<br /><br />0 = o índice foi criado pelo usuário.
|**optimize_for_sequential_key**|**bit**|1 = o índice tem a otimização de inserção da última página habilitada.<br><br>0 = valor padrão. O índice tem a otimização de inserção da última página desabilitada.|

> [!NOTE]
> Só há suporte para o bit **optimize_for_sequential_key** em versões SQL Server 2019 CTP 3,1 e superior.
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Para obter mais informações, consulte [configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os índices para `Production.Product` a tabela [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] no banco de dados.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys. index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys. xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [os grupos de sys. File&#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys. partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
