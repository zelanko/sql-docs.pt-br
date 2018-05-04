---
title: sys.dm_db_column_store_row_group_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_column_store_row_group_physical_stats_TSQL
- sys.dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_column_store_row_group_physical_stats
- sys.dm_db_column_store_row_group_physical_stats dynamic management view
caps.latest.revision: 15
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d52bceb3f67ba20c2abed4a06aa482d76ab1d307
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Fornece informações atuais de nível de grupo de linhas sobre todos os índices columnstore no banco de dados atual.  
  
 Isso estende a exibição de catálogo [column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|ID da tabela subjacente.|  
|**index_id**|**Int**|A ID desse índice columnstore em *object_id* tabela.|  
|**partition_number**|**Int**|ID da partição de tabela que contém *row_group_id*. Você pode usar o partition_number para adicionar esse DMV a sys.partitions.|  
|**row_group_id**|**Int**|ID deste grupo de linhas. Tabelas particionadas, isso é exclusivo dentro da partição.<br /><br /> -1 para uma final na memória.|  
|**delta_store_hobt_id**|**bigint**|O hobt_id para um grupo de linhas no repositório delta.<br /><br /> NULL se o grupo de linhas não está no repositório delta.<br /><br /> NULL para o final de uma tabela na memória.|  
|**state**|**tinyint**|O número de identificação associado *state_description*.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = DA MARCA DE EXCLUSÃO<br /><br /> COMPRESSED é o único estado que se aplica a tabelas na memória.|  
|**state_desc**|**nvarchar(60)**|Descrição do estado de grupo da linha:<br /><br /> INVISIBLE – um grupo de linhas que está sendo criado. Por exemplo: <br />Um grupo de linhas do ColumnStore é INVISÍVEL enquanto os dados estão sendo compactados. Terminada a compactação de um comutador de metadados é alterado o estado da linha columnstore grupo da INVISÍVEL compactada e o estado do grupo de linhas deltastore de fechado para exclusão.<br /><br /> OPEN – um grupo de linhas do deltastore que está aceitando novas linhas. Um grupo de linhas aberto ainda está no formato rowstore e não foi compactado para o formato columnstore.<br /><br /> CLOSED – um grupo de linhas no repositório delta que contém o número máximo de linhas e está aguardando que o processo de motor de tupla de compactá-las para o columnstore.<br /><br /> COMPRESSED – um grupo de linhas que é compactado com compactação columnstore e armazenado no columnstore.<br /><br /> TOMBSTONE – um grupo de linhas que foi anteriormente no deltastore e não seja usado.|  
|**total_rows**|**bigint**|Número de linhas físicos armazenado no grupo de linhas. Para grupos de linhas compactado, isso inclui as linhas que são marcados como excluídas.|  
|**deleted_rows**|**bigint**|Número de linhas fisicamente armazenados em um grupo de linhas compactados que são marcados para exclusão.<br /><br /> 0 para grupos de linhas que estão no repositório delta.|  
|**size_in_bytes**|**bigint**|Tamanho combinado, em bytes, de todas as páginas neste grupo de linhas. Esse tamanho não inclui o tamanho necessário para armazenar metadados ou dicionários compartilhados.|  
|**trim_reason**|**tinyint**|Motivo que disparou o grupo de linhas COMPACTADAS com menor que o número máximo de linhas.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1 - NO_TRIM<br /><br /> 2 - CARREGAMENTO EM MASSA<br /><br /> 3 – REORG<br /><br /> 4 – DICTIONARY_SIZE<br /><br /> 5 – MEMORY_LIMITATION<br /><br /> 6 – RESIDUAL_ROW_GROUP<br /><br /> 7 - STATS_MISMATCH<br /><br /> 8 - EXCEDENTE|  
|**trim_reason_desc**|**nvarchar(60)**|Descrição do *trim_reason*.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: ocorreu durante a atualização da versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 - NO_TRIM: O grupo de linhas não cortado. O grupo de linhas foi compactado com o máximo de 1,048,476 linhas.  O número de linhas pode ser menor se um subsset de linhas foi excluído depois que o rowgroup delta foi fechado<br /><br /> 2 – carregamento em MASSA: O tamanho do lote de carregamento em massa limitado o número de linhas.<br /><br /> 3 – REORG: Forçado compactação como parte do comando REORG.<br /><br /> 4 – DICTIONARY_SIZE: Tamanho do dicionário cresceu muito grande para compactar todas as linhas juntas.<br /><br /> 5 – MEMORY_LIMITATION: Não há memória disponível para compactar todas as linhas juntas.<br /><br /> 6 – RESIDUAL_ROW_GROUP: Fechado como parte do último grupo de linhas com milhões de linhas < 1 durante a operação de criação de índice<br /><br /> STATS_MISMATCH: somente para o columnstore na tabela na memória. Se as estatísticas incorretamente indicado > = 1 milhão de linhas qualificada no final, mas encontramos menos, o grupo de linhas compactado terá < 1 milhão de linhas<br /><br /> EXCEDENTE: apenas para o columnstore na tabela na memória. Se final tiver milhões de linhas qualificado > 1, as últimas linhas restantes do lote são compactadas se a contagem for entre 100 mil e 1 milhão|  
|**transition_to_compressed_state**|tinyint|Mostra como esse grupo de linhas foi movido de deltastore para um estado compactado no columnstore.<br /><br /> 1 - NOT_APPLICABLE<br /><br /> 2 – INDEX_BUILD<br /><br /> 3 – TUPLE_MOVER<br /><br /> 4 – REORG_NORMAL<br /><br /> 5 – REORG_FORCED<br /><br /> 6 - CARREGAMENTO EM MASSA<br /><br /> 7 - MERGE|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE – a operação não é aplicável para o deltastore. Ou, o rowgroup foi compactado antes da atualização para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] caso em que o histórico não é preservado.<br /><br /> Criação de um índice INDEX_BUILD – ou recompilação de índice compactado o grupo de linhas.<br /><br /> TUPLE_MOVER – o motor da tupla em execução em segundo plano compactados o grupo de linhas. Isso ocorre depois que o rowgroup mudará de aberto para o estado fechado.<br /><br /> REORG_NORMAL – a operação de reorganização, ALTER INDEX... REORGANIZAÇÃO, mover o grupo de linhas fechado do deltastore para o columnstore. Isso ocorreu antes do motor de tupla tido tempo para mover o grupo de linhas.<br /><br /> REORG_FORCED – este grupo de linhas foi aberto no deltastore e foi forçado para o columnstore antes de ele ter um número total de linhas.<br /><br /> Carregamento em MASSA – uma operação de carregamento em massa compactados rowgroup diretamente sem usar o deltastore.<br /><br /> MESCLAGEM – uma operação de mesclagem consolidados rowgroups de uma ou mais para este grupo de linhas e, em seguida, executada da compactação columnstore.|  
|**has_vertipaq_optimization**|bit|Otimização de Vertipaq melhora a compactação columnstore reorganizar a ordem das linhas no rowgroup para alcançar maior compactação. Essa otimização ocorre automaticamente na maioria dos casos. Há dois casos Vertipaq otimização não é usada:<br/>  A. Quando um rowgroup delta move para o columnstore e há um ou mais índices não clusterizados no índice columnstore - nesse caso Vertipaq otimização será ignorada para minimiza as alterações para o índice de mapeamento.<br/> B. para índices columnstore em tabelas com otimização de memória. <br /><br /> 0 = Não<br /><br /> 1 = Sim|  
|**Geração**|bigint|Geração de grupo de linha associada a este grupo de linhas.|  
|**created_time**|datetime2|Hora de quando esse grupo de linhas foi criado.<br /><br /> NULL – para um índice columnstore em uma tabela na memória.|  
|**closed_time**|datetime2|Hora de quando esse rowgroup foi fechado.<br /><br /> NULL – para um índice columnstore em uma tabela na memória.|  
  
## <a name="results"></a>Resultados  
 Retorna uma linha para cada grupo de linhas no banco de dados atual.  
  
## <a name="permissions"></a>Permissões  
 Requer estas permissões:  
  
-   Permissão CONTROL na tabela.  
  
-   Permissão VIEW DATABASE STATE no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. Calcule fragmentaton para decidir quando reorganizar ou recriar um índice columnstore.  
 Para índices columnstore, a porcentagem de linhas excluídas é uma medida válida para a fragmentação em um grupo de linhas. Quando a fragmentação é de 20% ou mais, é recomendável remover as linhas excluídas.  Para obter exemplos, consulte [desfragmentação de índices Columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md).  
  
 Este exemplo une **sys.DM db_column_store_row_group_physical_stats** com outros sistemas de tabelas e, em seguida, calcula o `Fragmentation` coluna como uma estimativa da eficiência de cada grupo de linhas no banco de dados atual.     Para localizar informações em uma única tabela, remova os hífens de comentário na frente do **onde** cláusula e forneça um nome de tabela.  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/total_rows AS 'Fragmentation'  
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guia de Índices Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
