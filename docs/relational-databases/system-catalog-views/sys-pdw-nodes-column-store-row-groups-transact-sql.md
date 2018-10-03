---
title: sys.pdw_nodes_column_store_row_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b3c09c2a1771f1fad8640031ea1c1327921f8c82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698234"
---
# <a name="syspdwnodescolumnstorerowgroups-transact-sql"></a>sys.pdw_nodes_column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Fornece informações de índice de columnstore clusterizado em uma base por segmento para ajudar o administrador a tomar decisões de gerenciamento de sistema [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. **sys.pdw_nodes_column_store_row_groups** tem uma coluna para o número total de linhas armazenadas fisicamente (inclusive as marcadas como excluídas) e uma coluna para o número de linhas marcadas como excluídas. Use **sys.pdw_nodes_column_store_row_groups** para determinar qual linha grupos têm uma alta porcentagem de linhas excluídas em devem ser recriados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela subjacente. Essa é a tabela física no nó de computação, não o object_id da tabela lógica no nó de controle. Por exemplo, object_id não coincide com o object_id em sys. Tables.<br /><br /> Para ingressar com Sys. Tables, use sys.pdw_index_mappings.|  
|**index_id**|**int**|ID do índice columnstore clusterizado em *object_id* tabela.|  
|**partition_number**|**int**|ID da partição de tabela que contém o grupo de linhas *row_group_id*. Você pode usar *partition_number* para adicionar esse DMV a sys. Partitions.|  
|**row_group_id**|**int**|ID nesse grupo de linhas. Isso é exclusivo dentro da partição.|  
|**dellta_store_hobt_id**|**bigint**|O hobt_id para grupos de linhas delta ou NULL se o tipo de grupo de linhas não for delta. Um grupo de linhas delta é um grupo de linhas de leitura/gravação que está aceitando novos registros. Um grupo de linhas delta tem o **abrir** status. Um grupo de linhas delta ainda está no formato rowstore e não foi compactado para o formato columnstore.|  
|**state**|**tinyint**|O número de ID associado a state_description.<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED|  
|**state_desccription**|**nvarchar(60)**|Descrição do estado persistente do grupo de linhas:<br /><br /> OPEN – Um grupo de linhas de leitura/gravação que está aceitando novos registros. Um grupo de linhas aberto ainda está no formato rowstore e não foi compactado para o formato columnstore.<br /><br /> CLOSED – Um grupo de linhas que foi preenchido, mas ainda não compactado pelo processo Tuple Mover.<br /><br /> COMPRESSED – Um grupo de linhas que foi preenchido e compactado.|  
|**total_rows**|**bigint**|Total de linhas fisicamente armazenadas no grupo de linhas. Algumas podem ter sido excluídas, mas ainda estão armazenadas. O número máximo de linhas em um grupo de linhas é 1.048.576 (FFFFF hexadecimal).|  
|**deleted_rows**|**bigint**|Número de linhas fisicamente armazenadas no grupo de linhas que são marcados para exclusão.<br /><br /> Sempre 0 para DELTA grupos de linhas.|  
|**size_in_bytes**|**int**|Tamanho combinado, em bytes, de todas as páginas nesse grupo de linhas. Esse tamanho não inclui o tamanho necessário para armazenar metadados ou dicionários compartilhados.|  
|**pdw_node_id**|**int**|Id exclusiva de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|  
|**distribution_id**|**int**|Id exclusiva da distribuição.|
  
## <a name="remarks"></a>Comentários  
 Retorna uma linha para cada grupo de linhas columnstore para cada tabela que tem um índice columnstore clusterizado ou não clusterizado.  
  
 Use **sys.pdw_nodes_column_store_row_groups** para determinar o número de linhas incluído no grupo de linhas e o tamanho do grupo de linhas.  
  
 Quando o número de linhas excluídas em um grupo de linhas cresce para uma grande porcentagem do total de linhas, a tabela fica menos eficiente. Recrie o índice columnstore para reduzir o tamanho da tabela, reduzindo a E/S de disco necessária para ler a tabela. Para recriar o índice columnstore, use o **recompile** opção do **ALTER INDEX** instrução.  
  
 O columnstore atualizável primeiro insere novos dados em um **abrir** rowgroup, o que está no formato rowstore e, às vezes também é conhecido como uma tabela delta.  Quando um rowgroup aberto está cheio, seu estado é alterado para **fechado**. Um rowgroup fechado é compactado no formato columnstore pelo tuple mover e o estado muda para **COMPRESSED**.  O Tuple Mover é um processo em segundo plano que periodicamente é acionado e verifica se há algum rowgroup fechado que já esteja pronto para compactar em um rowgroup columnstore.  O Tuple Mover também desaloca todos os rowgroups nos quais cada linha foi excluída. Rowgroups desalocados são marcados como **desativado**. Para executar o tuple mover imediatamente, use o **REORGANIZE** opção do **ALTER INDEX** instrução.  
  
 Quando um grupo de linhas de columnstore tiver sido preenchido, ele é compactado e para de aceitar novas linhas. Quando as linhas são excluídas de um grupo compactado, elas permanecem, mas são marcadas como excluídas. As atualizações para um grupo compactado são implementadas como uma exclusão do grupo compactado, e uma inserção em um grupo aberto.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **VIEW SERVER STATE**.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 A exemplo a seguir adiciona o **sys.pdw_nodes_column_store_row_groups** tabela a outras tabelas do sistema para retornar informações sobre tabelas específicas. A coluna calculada `PercentFull` é uma estimativa da eficiência do grupo de linhas. Para obter informações sobre uma única tabela, remova os hífens de comentário na frente da cláusula WHERE e forneça um nome de tabela.  
  
```  
SELECT IndexMap.object_id,   
  object_name(IndexMap.object_id) AS LogicalTableName,   
  i.name AS LogicalIndexName, IndexMap.index_id, NI.type_desc,   
  IndexMap.physical_name AS PhyIndexNameFromIMap,   
  CSRowGroups.*,  
  100*(ISNULL(deleted_rows,0))/total_rows AS PercentDeletedRows   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.pdw_index_mappings AS IndexMap  
    ON i.object_id = IndexMap.object_id  
    AND i.index_id = IndexMap.index_id  
JOIN sys.pdw_nodes_indexes AS NI  
    ON IndexMap.physical_name = NI.name  
    AND IndexMap.index_id = NI.index_id  
JOIN sys.pdw_nodes_column_store_row_groups AS CSRowGroups  
    ON CSRowGroups.object_id = NI.object_id   
    AND CSRowGroups.pdw_node_id = NI.pdw_node_id  
AND CSRowGroups.index_id = NI.index_id      
--WHERE t.name = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, IndexMap.physical_name, pdw_node_id;  
```  

O seguinte [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] exemplo conta as linhas por partição para coluna clusterizada armazena, bem como muitas linhas estiverem em grupos de aberto, fechado ou linha compactada:  

```
SELECT
    s.name AS [Schema Name]
    ,t.name AS [Table Name]
    ,rg.partition_number AS [Partition Number]
    ,SUM(rg.total_rows) AS [Total Rows]
    ,SUM(CASE WHEN rg.State = 1 THEN rg.Total_rows Else 0 END) AS [Rows in OPEN Row Groups]
    ,SUM(CASE WHEN rg.State = 2 THEN rg.Total_Rows ELSE 0 END) AS [Rows in Closed Row Groups]
    ,SUM(CASE WHEN rg.State = 3 THEN rg.Total_Rows ELSE 0 END) AS [Rows in COMPRESSED Row Groups]
FROM sys.pdw_nodes_column_store_row_groups rg
JOIN sys.pdw_nodes_tables pt
ON rg.object_id = pt.object_id AND rg.pdw_node_id = pt.pdw_node_id AND pt.distribution_id = rg.distribution_id
JOIN sys.pdw_table_mappings tm
ON pt.name = tm.physical_name
INNER JOIN sys.tables t
ON tm.object_id = t.object_id
INNER JOIN sys.schemas s
ON t.schema_id = s.schema_id
GROUP BY s.name, t.name, rg.partition_number
ORDER BY 1, 2
```
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
