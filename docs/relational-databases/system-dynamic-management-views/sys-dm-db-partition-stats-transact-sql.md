---
title: sys.dm_db_partition_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_partition_stats
- dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_partition_stats dynamic management view
ms.assetid: 9db9d184-b3a2-421e-a804-b18ebcb099b7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0221361bb3b2bb33748b20353c71931e07568f3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025090"
---
# <a name="sysdmdbpartitionstats-transact-sql"></a>sys.dm_db_partition_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de contagem de linhas e páginas para toda partição no banco de dados atual.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **DM pdw_nodes_db_partition_stats**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|ID da partição. É exclusiva em um banco de dados. Isso é o mesmo valor que o **partition_id** na **sys. Partitions** exibição do catálogo|  
|**object_id**|**int**|ID de objeto da tabela ou exibição indexada da qual a partição faz parte.|  
|**index_id**|**int**|ID do heap ou índice do qual a partição faz parte.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado.<br /><br /> > 1 = índice não clusterizado|  
|**partition_number**|**int**|Número de partição com base 1 no índice ou heap.|  
|**in_row_data_page_count**|**bigint**|Número de páginas em uso para armazenar dados em linha nesta partição. Se a partição fizer parte de um heap, o valor será o número de páginas de dados no heap. Se a partição fizer parte de um índice, o valor será o número de páginas no nível folha. (Páginas não folha na árvore B não são incluídas na contagem.) As páginas IAM (Index Allocation Map) não são incluídas em ambos os casos. Sempre 0 para um índice columnstore xVelocity de memória otimizada.|  
|**in_row_used_page_count**|**bigint**|Número total de páginas em uso para armazenar e gerenciar os dados em linha nesta partição. Essa contagem inclui páginas não folha de árvore B, as páginas IAM e todas as páginas incluídas na **in_row_data_page_count** coluna. Sempre 0 para um índice columnstore.|  
|**in_row_reserved_page_count**|**bigint**|Número total de páginas reservadas para armazenar e gerenciar dados em linha nesta partição, independentemente do fato de as páginas estarem ou não em uso. Sempre 0 para um índice columnstore.|  
|**lob_used_page_count**|**bigint**|Número de páginas em uso para armazenar e gerenciar fora de linha **texto**, **ntext**, **imagem**, **varchar (max)**, **nvarchar (máx.)** , **varbinary (max)**, e **xml** colunas dentro da partição. As páginas IAM são incluídas.<br /><br /> Número total de LOBs usados para armazenar e gerenciar o índice columnstore na partição.|  
|**lob_reserved_page_count**|**bigint**|Número total de páginas reservadas para armazenar e gerenciar fora de linha **texto**, **ntext**, **imagem**, **varchar (max)**,  **nvarchar (max)**, **varbinary (max)**, e **xml** colunas dentro da partição, independentemente se as páginas estão em uso ou não. As páginas IAM são incluídas.<br /><br /> Número total de LOBs reservados para armazenar e gerenciar o índice columnstore na partição.|  
|**row_overflow_used_page_count**|**bigint**|Número de páginas em uso para armazenar e gerenciar o estouro de linha **varchar**, **nvarchar**, **varbinary**, e **sql_variant** colunas dentro da partição. As páginas IAM são incluídas.<br /><br /> Sempre 0 para um índice columnstore.|  
|**row_overflow_reserved_page_count**|**bigint**|Número total de páginas reservadas para armazenar e gerenciar o estouro de linha **varchar**, **nvarchar**, **varbinary**, e **sql_variant** colunas dentro da partição, independentemente se as páginas estão em uso ou não. As páginas IAM são incluídas.<br /><br /> Sempre 0 para um índice columnstore.|  
|**used_page_count**|**bigint**|Número total de páginas usadas para a partição. Computado como **in_row_used_page_count** + **lob_used_page_count** + **row_overflow_used_page_count**.|  
|**reserved_page_count**|**bigint**|Número total de páginas reservadas para a partição. Computado como **in_row_reserved_page_count** + **lob_reserved_page_count** + **row_overflow_reserved_page_count**.|  
|**row_count**|**bigint**|O número aproximado de linhas na partição.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
|**distribution_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> A id numérica exclusiva associada à distribuição.|  
  
## <a name="remarks"></a>Comentários  
 **DM db_partition_stats** exibe informações sobre o espaço usado para armazenar e gerenciar dados LOB de dados em linha e dados de estouro de linha para todas as partições em um banco de dados. É exibida uma linha por partição.  
  
 As contagens nas quais a saída tem como base são armazenadas em cache na memória ou armazenadas em disco nas diversas tabelas do sistema.  
  
 Dados em linha, dados LOB e dados de estouro de linha representam as três unidades de alocação que compõem uma partição. O [sys. allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) exibição de catálogo pode ser consultada por metadados sobre cada unidade de alocação no banco de dados.  
  
 Se um heap ou índice não for particionado, ele será composto de uma partição (com número de partição = 1); portanto, somente uma linha será retornada para esse heap ou índice. O [sys. Partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) exibição do catálogo pode ser consultada por metadados sobre cada partição de todas as tabelas e índices em um banco de dados.  
  
 A contagem total para uma tabela ou índice individual pode ser obtida pela adição das contagens de todas as partições relevantes.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão VIEW DATABASE STATE para consultar o **DM db_partition_stats** exibição de gerenciamento dinâmico. Para obter mais informações sobre permissões de exibições de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-all-counts-for-all-partitions-of-all-indexes-and-heaps-in-a-database"></a>A. Retornando todas as contagens de todas as partições de todos os índices e heaps em um banco de dados  
 O exemplo a seguir mostra todas as contagens de todas as partições de todos os índices e heaps no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats;  
GO  
```  
  
### <a name="b-returning-all-counts-for-all-partitions-of-a-table-and-its-indexes"></a>B. Retornando todas as contagens de todas as partições de uma tabela e seus índices  
 O exemplo a seguir mostra todas as contagens de todas as partições da tabela `HumanResources.Employee` e seus índices.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats   
WHERE object_id = OBJECT_ID('HumanResources.Employee');  
GO  
```  
  
### <a name="c-returning-total-used-pages-and-total-number-of-rows-for-a-heap-or-clustered-index"></a>C. Retornando o total de páginas usadas e número total de linhas para um heap ou índice clusterizado  
 O exemplo a seguir retorna o total de páginas usadas e o número total de linhas para o heap ou índice clusterizado da tabela `HumanResources.Employee`. Como a tabela `Employee` não é particionada por padrão, observe que a soma inclui somente uma partição.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SUM(used_page_count) AS total_number_of_used_pages,   
    SUM (row_count) AS total_number_of_rows   
FROM sys.dm_db_partition_stats  
WHERE object_id=OBJECT_ID('HumanResources.Employee')    AND (index_id=0 or index_id=1);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  


