---
title: sys.dm_db_column_store_row_group_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f725ca776fcc65828c7f72b4e3c2b042d0203b71
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742042"
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Fornece informações de nível de grupo de linhas atuais sobre todos os índices columnstore no banco de dados atual.  
  
 Isso estende a exibição do catálogo [column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela subjacente.|  
|**index_id**|**int**|A ID desse índice columnstore na *object_id* tabela.|  
|**partition_number**|**int**|ID da partição de tabela que contém *row_group_id*. Você pode usar o partition_number para adicionar esse DMV a sys.partitions.|  
|**row_group_id**|**int**|ID nesse grupo de linhas. Tabelas particionadas, isso é exclusivo dentro da partição.<br /><br /> -1 para um final na memória.|  
|**delta_store_hobt_id**|**bigint**|O hobt_id para um grupo de linhas no repositório delta.<br /><br /> NULL se o grupo de linhas não está no repositório delta.<br /><br /> NULL para o final de uma tabela na memória.|  
|**state**|**tinyint**|Número de identificação associado *state_description*.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = DA MARCA PARA EXCLUSÃO<br /><br /> COMPRESSED é o único estado que se aplica a tabelas na memória.|  
|**state_desc**|**nvarchar(60)**|Descrição do estado do grupo de linhas:<br /><br /> INVISÍVEL - um grupo de linhas que está sendo criado. Por exemplo:  <br />Um grupo de linhas no columnstore é INVISÍVEL, enquanto os dados estão sendo compactados. Quando a compactação é concluída em um comutador de metadados é alterado o estado da linha columnstore grupo da INVISÍVEL compactada e o estado do grupo de linhas deltastore de fechado para marca de exclusão.<br /><br /> Abra - um grupo de linhas do deltastore que está aceitando novas linhas. Um grupo de linhas aberto ainda está no formato rowstore e não foi compactado para o formato columnstore.<br /><br /> FECHADO – um grupo de linhas no repositório delta que contém o número máximo de linhas e está aguardando o processo de motor de tupla para compactá-lo no columnstore.<br /><br /> COMPACTADOS - um grupo de linhas que é compactado com compactação columnstore e armazenado no columnstore.<br /><br /> Marca para exclusão – um grupo de linhas que estava anteriormente no deltastore e não é mais usado.|  
|**total_rows**|**bigint**|Número de linhas físicas armazenado no grupo de linhas. Para grupos de linhas compactados, isso inclui as linhas que são marcados como excluídas.|  
|**deleted_rows**|**bigint**|Número de linhas fisicamente armazenados em um grupo de linhas compactados que são marcados para exclusão.<br /><br /> 0 para grupos de linhas que estão no repositório delta.|  
|**size_in_bytes**|**bigint**|Tamanho combinado, em bytes, de todas as páginas nesse grupo de linhas. Esse tamanho não inclui o tamanho necessário para armazenar metadados ou dicionários compartilhados.|  
|**trim_reason**|**tinyint**|Motivo que disparou o grupo de linhas COMPACTADAS ter menor que o número máximo de linhas.<br /><br /> 0 - UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1 - NO_TRIM<br /><br /> 2 - CARREGAMENTO EM MASSA<br /><br /> 3 - REORG<br /><br /> 4 - DICTIONARY_SIZE<br /><br /> 5 - MEMORY_LIMITATION<br /><br /> 6 - RESIDUAL_ROW_GROUP<br /><br /> 7  -  STATS_MISMATCH<br /><br /> 8 - EXCEDENTE|  
|**trim_reason_desc**|**nvarchar(60)**|Descrição da *trim_reason*.<br /><br /> 0 - UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: Ocorreu durante a atualização da versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 - NO_TRIM: O grupo de linhas não foi cortado. O grupo de linhas foi compactado com o máximo de 1,048,476 linhas.  O número de linhas pode ser menor se um subsset de linhas foi excluído depois que o rowgroup delta foi fechado<br /><br /> 2 - CARREGAMENTO EM MASSA: O tamanho do lote de carregamento em massa limitado o número de linhas.<br /><br /> 3 - REORG:  Forçado a compactação como parte do comando REORG.<br /><br /> 4 - DICTIONARY_SIZE: Tamanho do dicionário cresceu muito grande para compactar todas as linhas juntas.<br /><br /> 5 - MEMORY_LIMITATION: Memória insuficiente disponível para compactar todas as linhas juntas.<br /><br /> 6 - RESIDUAL_ROW_GROUP:  Fechado como parte do último grupo de linhas com milhões de linhas < 1 durante a operação de compilação de índice<br /><br /> STATS_MISMATCH: Somente para o columnstore na tabela na memória. Se estatísticas incorretamente indicado > = 1 milhão de linhas qualificadas na cauda, mas encontramos menos, o rowgroup compactado terá < 1 milhão de linhas<br /><br /> EXCEDENTE: Somente para o columnstore na tabela na memória. Se o final tem milhões de linhas qualificado > 1, as últimas linhas restantes do lote são compactadas se a contagem é entre 100 mil e 1 milhão|  
|**transition_to_compressed_state**|TINYINT|Mostra como esse grupo de linhas foi movido de deltastore para um estado compactado no columnstore.<br /><br /> 1- NOT_APPLICABLE<br /><br /> 2 - INDEX_BUILD<br /><br /> 3 - TUPLE_MOVER<br /><br /> 4 - REORG_NORMAL<br /><br /> 5 - REORG_FORCED<br /><br /> 6 - CARREGAMENTO EM MASSA<br /><br /> 7 - MESCLAGEM|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE - a operação não é aplicável para o deltastore. Ou, o rowgroup foi compactado antes da atualização para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] caso em que o histórico não será preservado.<br /><br /> Criar de um índice INDEX_BUILD - ou recompilação de índice compactado o grupo de linhas.<br /><br /> TUPLE_MOVER - o motor de tupla em execução em segundo plano compactados do rowgroup. Isso acontece depois que o rowgroup mudará de aberto para o estado fechado.<br /><br /> REORG_NORMAL - a operação de reorganização, ALTER INDEX... REORGANIZAÇÃO, movido o rowgroup CLOSED do deltastore para o columnstore. Isso ocorreu antes do motor de tupla teve tempo para mover o grupo de linhas.<br /><br /> REORG_FORCED - esse grupo de linhas foi aberto no deltastore e foi forçado para o columnstore antes que ele tinha um número total de linhas.<br /><br /> Carregamento em MASSA - uma operação de carregamento em massa compactados rowgroup diretamente sem usar o deltastore.<br /><br /> MESCLAGEM – executada, em seguida, a compactação columnstore e consolidados de um ou mais rowgroups nesse grupo de linhas de uma operação de mesclagem.|  
|**has_vertipaq_optimization**|bit|A otimização de Vertipaq melhora a compactação columnstore reorganizar a ordem das linhas no rowgroup para alcançar uma compactação maior. Essa otimização acontece automaticamente na maioria dos casos. Há dois casos Vertipaq otimização não é usada:<br/>  a. Quando um rowgroup delta move para o columnstore e há um ou mais índices não clusterizados no índice columnstore - nesse caso, otimização de Vertipaq é ignorada para minimiza as alterações para o índice de mapeamento;<br/> b. para índices columnstore em tabelas com otimização de memória. <br /><br /> 0 = Não<br /><br /> 1 = Sim|  
|**generation**|BIGINT|Geração de grupo de linha associada a este grupo de linhas.|  
|**created_time**|datetime2|Hora em que esse grupo de linhas foi criado.<br /><br /> NULO - para um índice columnstore em uma tabela na memória.|  
|**closed_time**|datetime2|Hora em que esse grupo de linhas foi fechado.<br /><br /> NULO - para um índice columnstore em uma tabela na memória.|  
  
## <a name="results"></a>Resultados  
 Retorna uma linha para cada grupo de linhas no banco de dados atual.  
  
## <a name="permissions"></a>Permissões  
 Requer estas permissões:  
  
-   Permissão CONTROL na tabela.  
  
-   Permissão VIEW DATABASE STATE no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. Calcule fragmentaton para decidir quando reorganizar ou recompilar um índice columnstore.  
 Para índices columnstore, a porcentagem de linhas excluídas é uma boa medida para a fragmentação em um grupo de linhas. Quando a fragmentação é de 20% ou mais, é recomendável remover as linhas excluídas.  Para obter exemplos, consulte [desfragmentação de índices Columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md).  
  
 Este exemplo une **DM db_column_store_row_group_physical_stats** com outro sistema tabelas e, em seguida, calcula o `Fragmentation` coluna como uma estimativa da eficiência de cada grupo de linhas no banco de dados atual.     Para localizar informações em uma única tabela, remova os hífens de comentário na frente do **onde** cláusula e forneça um nome de tabela.  
  
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
  
