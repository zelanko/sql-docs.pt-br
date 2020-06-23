---
title: sys. dm_db_column_store_row_group_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fcfbbfb755892d710fef45554a87492ca2c37339
ms.sourcegitcommit: d498110ec0c7c62782fb694d14436f06681f2c30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2020
ms.locfileid: "85196053"
---
# <a name="sysdm_db_column_store_row_group_physical_stats-transact-sql"></a>sys. dm_db_column_store_row_group_physical_stats (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Fornece informações atuais em nível de rowgroup sobre todos os índices columnstore no banco de dados atual.  

Isso estende a exibição de catálogo [Sys. column_store_row_groups &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md).  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela subjacente.|  
|**index_id**|**int**|ID deste índice columnstore na tabela *object_id* .|  
|**partition_number**|**int**|ID da partição de tabela que contém *row_group_id*. Você pode usar o partition_number para adicionar esse DMV a sys.partitions.|  
|**row_group_id**|**int**|ID deste grupo de linhas. Para tabelas particionadas, o valor é exclusivo na partição.<br /><br /> -1 para uma parte final da memória.|  
|**delta_store_hobt_id**|**bigint**|O hobt_id para um grupo de linhas no armazenamento Delta.<br /><br /> NULL se o grupo de linhas não estiver no repositório Delta.<br /><br /> NULL para a parte final de uma tabela na memória.|  
|**state**|**tinyint**|Número de ID associado *state_description*.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = MARCA PARA EXCLUSÃO<br /><br /> COMPACTado é o único Estado que se aplica a tabelas na memória.|  
|**state_desc**|**nvarchar(60)**|Descrição do estado do grupo de linhas:<br /><br /> 0-invisível-um grupo de linhas que está sendo compilado. Por exemplo: <br />Um grupo de linhas no columnstore é invisível enquanto os dados estão sendo compactados. Quando a compactação é concluída, uma opção de metadados altera o estado do grupo de linhas columnstore de invisível para COMPACTado e o estado do grupo de linhas deltastore de CLOSED para marca para exclusão.<br /><br /> 1-abrir um grupo de linhas deltastore que está aceitando novas linhas. Um grupo de linhas aberto ainda está no formato rowstore e não foi compactado para o formato columnstore.<br /><br /> 2-CLOSED-um grupo de linhas no repositório Delta que contém o número máximo de linhas e está aguardando o processo de movimentação de tupla compactá-lo no columnstore.<br /><br /> 3-COMPACTado-um grupo de linhas que é compactado com compactação columnstore e armazenado no columnstore.<br /><br /> 4-marcas de exclusão – um grupo de linhas que estava anteriormente no deltastore e que não é mais usado.|  
|**total_rows**|**bigint**|Número de linhas fisicamente armazenadas no grupo de linhas. Para grupos de linhas compactados. Inclui as linhas marcadas como excluídas.|  
|**deleted_rows**|**bigint**|Número de linhas fisicamente armazenadas em um grupo de linhas compactado que são marcadas para exclusão.<br /><br /> 0 para grupos de linhas que estão no repositório Delta.|  
|**size_in_bytes**|**bigint**|Tamanho combinado, em bytes, de todas as páginas deste grupo de linhas. Esse tamanho não inclui o tamanho necessário para armazenar metadados ou dicionários compartilhados.|  
|**trim_reason**|**tinyint**|Motivo que disparou o grupo de linhas COMPACTado para ter menos do que o número máximo de linhas.<br /><br /> 0-UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1-NO_TRIM<br /><br /> 2-CARREGAMENTO EM MASSA<br /><br /> 3-REORG<br /><br /> 4-DICTIONARY_SIZE<br /><br /> 5-MEMORY_LIMITATION<br /><br /> 6-RESIDUAL_ROW_GROUP<br /><br /> 7-STATS_MISMATCH<br /><br /> 8-EXCEDENTE<br /><br /> 9-AUTO_MERGE|  
|**trim_reason_desc**|**nvarchar(60)**|Descrição de *trim_reason*.<br /><br /> 0-UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: ocorreu ao atualizar da versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> 1-NO_TRIM: o grupo de linhas não foi cortado. O grupo de linhas foi compactado com o máximo de 1.048.476 linhas.  O número de linhas pode ser menor se um subconjunto de linhas tiver sido excluído depois que o rowgroup Delta tiver sido fechado<br /><br /> 2-carregamento em massa: o tamanho do lote de carregamento em massa limitou o número de linhas.<br /><br /> 3-REORG: compactação forçada como parte do comando REORG.<br /><br /> 4-DICTIONARY_SIZE: o tamanho do dicionário cresceu muito grande para compactar todas as linhas juntas.<br /><br /> 5-MEMORY_LIMITATION: não há memória suficiente disponível para compactar todas as linhas juntas.<br /><br /> 6-RESIDUAL_ROW_GROUP: fechada como parte do último grupo de linhas com linhas < 1 milhão durante a operação de compilação do índice<br /><br /> 7-STATS_MISMATCH: somente para columnstore na tabela na memória. Se as estatísticas indicaram incorretamente >= 1 milhão linhas qualificadas na parte final, mas encontramos menos, o rowgroup compactado terá < 1 milhão linhas<br /><br /> 8-excedente: somente para o columnstore na tabela na memória. Se a parte final tiver > 1 milhão linhas qualificadas, as linhas do último lote restante serão compactadas se a contagem estiver entre 100 mil e 1 milhão<br /><br /> 9-AUTO_MERGE: uma operação de mesclagem de movimentação de tupla em execução em segundo plano consolidou um ou mais grupos de rowgroup nesse rowgroup.|  
|**transition_to_compressed_state**|TINYINT|Mostra como esse rowgroup foi movido do deltastore para um estado compactado no columnstore.<br /><br /> 1-NOT_APPLICABLE<br /><br /> 2-INDEX_BUILD<br /><br /> 3-TUPLE_MOVER<br /><br /> 4-REORG_NORMAL<br /><br /> 5-REORG_FORCED<br /><br /> 6-CARREGAMENTO EM MASSA<br /><br /> 7-MESCLAR|  
|**transition_to_compressed_state_desc**|nvarchar(60)| 1-NOT_APPLICABLE-a operação não se aplica ao deltastore. Ou, o rowgroup foi compactado antes da atualização para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] o caso em que o histórico não é preservado.<br /><br /> 2-INDEX_BUILD-uma criação de índice ou uma recompilação de índice comprimiu o rowgroup.<br /><br /> 3-TUPLE_MOVER-o movimentador de tupla em execução em segundo plano compactou o rowgroup. O motor da tupla ocorre depois que o estado de alterações do rowgroup é aberto para fechado.<br /><br /> 4-REORG_NORMAL-a operação de reorganização, ALTER INDEX... REORG, moveu o rowgroup fechado do deltastore para o columnstore. Isso ocorreu antes que o motor de tupla tivesse tempo para mover o rowgroup.<br /><br /> 5-REORG_FORCED-esse rowgroup estava aberto no deltastore e foi forçado para o columnstore antes de ter um número completo de linhas.<br /><br /> 6-carregamento em massa-uma operação de carregamento em massa compactou o rowgroup diretamente sem usar o deltastore.<br /><br /> 7-MERGE-uma operação de mesclagem consolidou um ou mais grupos de rowgroup nesse rowgroup e, em seguida, executou a compactação columnstore.|  
|**has_vertipaq_optimization**|bit|A otimização de VertiPaq melhora a compactação de columnstore reorganizando a ordem das linhas no rowgroup para obter maior compactação. Essa otimização ocorre automaticamente na maioria dos casos. Há dois casos em que a otimização VertiPaq não é usada:<br/>  a. Quando um rowgroup Delta se move para o columnstore e há um ou mais índices não clusterizados no índice columnstore – nesse caso, a otimização de VertiPaq é ignorada para minimizar as alterações no índice de mapeamento;<br/> b. para índices columnstore em tabelas com otimização de memória. <br /><br /> 0 = Não<br /><br /> 1 = Sim|  
|**geração**|BIGINT|Geração de grupo de linhas associada a este grupo de linhas.|  
|**created_time**|datetime2|Hora do relógio para quando esse rowgroup foi criado.<br /><br /> NULL-para um índice columnstore em uma tabela na memória.|  
|**closed_time**|datetime2|Hora do relógio para quando este rowgroup foi fechado.<br /><br /> NULL-para um índice columnstore em uma tabela na memória.|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="results"></a>Resultados  
 Retorna uma linha para cada rowgroup no banco de dados atual.  
  
## <a name="permissions"></a>Permissões  
Requer `CONTROL` a permissão na tabela e a `VIEW DATABASE STATE` permissão no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calculate-fragmentation-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>a. Calcule a fragmentação para decidir quando reorganizar ou recriar um índice columnstore.  
 Para índices columnstore, a porcentagem de linhas excluídas é uma boa medida para a fragmentação em um rowgroup. Quando a fragmentação for de 20% ou mais, remova as linhas excluídas. Para obter mais exemplos, consulte [reorganizar e recompilar índices](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Este exemplo une **Sys. dm_db_column_store_row_group_physical_stats** a outras tabelas do sistema e, em seguida, calcula a `Fragmentation` coluna como uma estimativa da eficiência de cada grupo de linhas no banco de dados atual. Para localizar informações em uma única tabela, remova os hifens de comentário na frente da cláusula **Where** e forneça um nome de tabela.  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0) AS 'Fragmentation'
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)      
 [Arquitetura de índices columnstore](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)         
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [&#41;sys. Columns &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys. computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
 [sys. column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
