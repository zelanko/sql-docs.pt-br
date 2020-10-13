---
description: sys.dm_db_partition_stats (Transact-SQL)
title: sys.dm_db_partition_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a1fd58cef1e99a1c7648ea8ad73657b7dc02be01
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006015"
---
# <a name="sysdm_db_partition_stats-transact-sql"></a>sys.dm_db_partition_stats (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna informações de contagem de linhas e páginas para toda partição no banco de dados atual.  
  
> [!NOTE]  
> Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys.dm_pdw_nodes_db_partition_stats**. A partition_id em sys.dm_pdw_nodes_db_partition_stats difere da partition_id na exibição de catálogo sys. partitions do Azure Synapse Analytics.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|ID da partição. É exclusiva em um banco de dados. Esse é o mesmo valor que o **partition_id** na exibição de catálogo **Sys. partitions** , exceto para o Azure Synapse Analytics.|  
|**object_id**|**int**|ID de objeto da tabela ou exibição indexada da qual a partição faz parte.|  
|**index_id**|**int**|ID do heap ou índice do qual a partição faz parte.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado.<br /><br /> >1 = Índice não clusterizado|  
|**partition_number**|**int**|Número de partição com base 1 no índice ou heap.|  
|**in_row_data_page_count**|**bigint**|Número de páginas em uso para armazenar dados em linha nesta partição. Se a partição fizer parte de um heap, o valor será o número de páginas de dados no heap. Se a partição fizer parte de um índice, o valor será o número de páginas no nível folha. (As páginas não folha na árvore B não são incluídas na contagem.) As páginas IAM (mapa de alocação de índice) não são incluídas em nenhum dos casos. Sempre 0 para um índice columnstore xVelocity de memória otimizada.|  
|**in_row_used_page_count**|**bigint**|Número total de páginas em uso para armazenar e gerenciar os dados em linha nesta partição. Essa contagem inclui páginas não folha da árvore B, páginas IAM e todas as páginas incluídas na coluna **in_row_data_page_count**. Sempre 0 para um índice columnstore.|  
|**in_row_reserved_page_count**|**bigint**|Número total de páginas reservadas para armazenar e gerenciar dados em linha nesta partição, independentemente do fato de as páginas estarem ou não em uso. Sempre 0 para um índice columnstore.|  
|**lob_used_page_count**|**bigint**|Número de páginas em uso para armazenar e gerenciar colunas **text**, **ntext**, **image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)** e **xml** fora de linha na partição. As páginas IAM são incluídas.<br /><br /> Número total de LOBs usados para armazenar e gerenciar o índice columnstore na partição.|  
|**lob_reserved_page_count**|**bigint**|Número total de páginas reservadas para armazenar e gerenciar colunas **text**, **ntext**, **image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)** e **xml** fora de linha na partição, independentemente do fato de as páginas estarem ou não em uso. As páginas IAM são incluídas.<br /><br /> Número total de LOBs reservados para armazenar e gerenciar o índice columnstore na partição.|  
|**row_overflow_used_page_count**|**bigint**|Número de páginas em uso para armazenar e gerenciar colunas **varchar**, **nvarchar**, **varbinary** e **sql_variant** na partição. As páginas IAM são incluídas.<br /><br /> Sempre 0 para um índice columnstore.|  
|**row_overflow_reserved_page_count**|**bigint**|Número total de páginas reservadas para armazenar e gerenciar colunas **varchar**, **nvarchar**, **varbinary** e **sql_variant** excedentes de linha na partição, independentemente do fato de as páginas estarem ou não em uso. As páginas IAM são incluídas.<br /><br /> Sempre 0 para um índice columnstore.|  
|**used_page_count**|**bigint**|Número total de páginas usadas para a partição. Calculado como **in_row_used_page_count**  +  **lob_used_page_count**  +  **row_overflow_used_page_count**.|  
|**reserved_page_count**|**bigint**|Número total de páginas reservadas para a partição. Calculado como **in_row_reserved_page_count**  +  **lob_reserved_page_count**  +  **row_overflow_reserved_page_count**.|  
|**row_count**|**bigint**|O número aproximado de linhas na partição.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
|**distribution_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> A ID numérica exclusiva associada à distribuição.|  
  
## <a name="remarks"></a>Comentários  
 **sys.dm_db_partition_stats** exibe informações sobre o espaço usado para armazenar e gerenciar dados LOB de dados em linha e dados de estouro de linha para todas as partições em um banco de dados. É exibida uma linha por partição.  
  
 As contagens nas quais a saída tem como base são armazenadas em cache na memória ou armazenadas em disco nas diversas tabelas do sistema.  
  
 Dados em linha, dados LOB e dados de estouro de linha representam as três unidades de alocação que compõem uma partição. A exibição de catálogo [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) pode ser consultada por metadados sobre cada unidade de alocação no banco de dados.  
  
 Se um heap ou índice não for particionado, ele será composto de uma partição (com número de partição = 1); portanto, somente uma linha será retornada para esse heap ou índice. A exibição de catálogo [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) pode ser consultada por metadados sobre cada partição de todas as tabelas e índices em um banco de dados.  
  
 A contagem total para uma tabela ou índice individual pode ser obtida pela adição das contagens de todas as partições relevantes.  
  
## <a name="permissions"></a>Permissões  
 Requer `VIEW DATABASE STATE` e `VIEW DEFINITION` permissões para consultar a exibição de gerenciamento dinâmico **Sys.dm_db_partition_stats** . Para obter mais informações sobre permissões em exibições de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;&#41;Transact-SQL ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-all-counts-for-all-partitions-of-all-indexes-and-heaps-in-a-database"></a>a. Retornando todas as contagens de todas as partições de todos os índices e heaps em um banco de dados  
 O exemplo a seguir mostra todas as contagens de todas as partições de todos os índices e heaps no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats;  
GO  
```  
  
### <a name="b-returning-all-counts-for-all-partitions-of-a-table-and-its-indexes"></a>B. Retornando todas as contagens de todas as partições de uma tabela e seus índices  
 O exemplo a seguir mostra todas as contagens de todas as partições da tabela `HumanResources.Employee` e seus índices.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats   
WHERE object_id = OBJECT_ID('HumanResources.Employee');  
GO  
```  
  
### <a name="c-returning-total-used-pages-and-total-number-of-rows-for-a-heap-or-clustered-index"></a>C. Retornando o total de páginas usadas e número total de linhas para um heap ou índice clusterizado  
 O exemplo a seguir retorna o total de páginas usadas e o número total de linhas para o heap ou índice clusterizado da tabela `HumanResources.Employee`. Como a tabela `Employee` não é particionada por padrão, observe que a soma inclui somente uma partição.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT SUM(used_page_count) AS total_number_of_used_pages,   
    SUM (row_count) AS total_number_of_rows   
FROM sys.dm_db_partition_stats  
WHERE object_id=OBJECT_ID('HumanResources.Employee')    AND (index_id=0 or index_id=1);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  


