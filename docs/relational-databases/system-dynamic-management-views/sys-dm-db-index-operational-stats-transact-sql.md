---
description: sys.dm_db_index_operational_stats (Transact-SQL)
title: sys.dm_db_index_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_operational_stats
- sys.dm_db_index_operational_stats_TSQL
- sys.dm_db_index_operational_stats
- dm_db_index_operational_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_operational_stats dynamic management function
ms.assetid: 13adf2e5-2150-40a6-b346-e74a33ce29c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1f177d09dd741eadc967a2b32a87a905e04dfb6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475067"
---
# <a name="sysdm_db_index_operational_stats-transact-sql"></a>sys.dm_db_index_operational_stats (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna a atividade atual de e/s de nível inferior, bloqueio, trava e método de acesso para cada partição de uma tabela ou índice no banco de dados.    
    
 Os índices com otimização de memória não aparecem nessa DMV.    
    
> [!NOTE]    
>  **Sys.dm_db_index_operational_stats** não retorna informações sobre índices com otimização de memória. Para obter informações sobre o uso de índice com otimização de memória, consulte [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md).    
        
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxe    
    
```    
sys.dm_db_index_operational_stats (    
    { database_id | NULL | 0 | DEFAULT }    
  , { object_id | NULL | 0 | DEFAULT }    
  , { index_id | 0 | NULL | -1 | DEFAULT }    
  , { partition_number | NULL | 0 | DEFAULT }    
)    
```    
    
## <a name="arguments"></a>Argumentos    

*database_id* | NULL | 0 | OS

  ID do banco de dados. *database_id* é **smallint**. As entradas válidas são o número da ID de um banco de dados, NULL, 0 ou DEFAULT. O padrão é 0. NULL, 0 e DEFAULT são valores equivalentes neste contexto.    
    
 Especifique NULL para retornar informações de todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar NULL para *database_id*, também deverá especificar null para *object_id*, *index_id* e *partition_number*.    
    
 A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificada.    

*object_id* | NULL | 0 | OS

 ID do objeto da tabela ou exibição em que o índice está ativado. *object_id* é **int**.    
    
 As entradas válidas são o número da ID de uma tabela e de uma exibição, NULL, 0 ou DEFAULT. O padrão é 0. NULL, 0 e DEFAULT são valores equivalentes neste contexto.    
    
 Especifique NULL para retornar informações em cache de todas as tabelas e exibições no banco de dados especificado. Se você especificar NULL para *object_id*, também deverá especificar null para *index_id* e *partition_number*.    

*index_id* | 0 | NULL | -1 | OS

 ID do índice. *index_id* é **int**. As entradas válidas são o número de identificação de um índice, 0 se *object_id* for um heap, nulo,-1 ou padrão. O padrão é -1, NULL, -1 e DEFAULT são valores equivalentes neste contexto.    
    
 Especifique NULL para retornar informações em cache de todos os índices de uma tabela base ou exibição. Se você especificar NULL para *index_id*, também deverá especificar null para *partition_number*.    

*partition_number* | NULL | 0 | OS

 O número da partição no objeto. *partition_number* é **int**. As entradas válidas são a *partion_number* de um índice ou heap, NULL, 0 ou default. O padrão é 0. NULL, 0 e DEFAULT são valores equivalentes neste contexto.    
    
 Especifique NULL para retornar informações em cache de todas as partições do índice ou heap.    
    
 o *partition_number* é baseado em 1. Um índice ou heap não particionado tem *partition_number* definido como 1.    
    
## <a name="table-returned"></a>Tabela retornada    
    
|Nome da coluna|Tipo de dados|Descrição|    
|-----------------|---------------|-----------------|    
|**database_id**|**smallint**|ID do banco de dados.|    
|**object_id**|**int**|ID da tabela ou exibição.|    
|**index_id**|**int**|ID do índice ou heap.<br /><br /> 0 = Heap| 
|**partition_number**|**int**|Número de partição com base 1 no índice ou heap.| 
|**hobt_id**|**bigint**|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](../../sql-server/what-s-new-in-sql-server-2016.md)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .<br /><br /> ID do conjunto de linhas de heap ou árvore B de dados que controla dados internos para um índice columnstore.<br /><br /> NULL-este não é um conjunto de linhas columnstore interno.<br /><br /> Para obter mais detalhes, consulte [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)|       
|**leaf_insert_count**|**bigint**|Contagem cumulativa de inserções de nível folha.|    
|**leaf_delete_count**|**bigint**|Contagem cumulativa de exclusões de nível folha. leaf_delete_count é incrementado apenas para registros excluídos que não são marcados como fantasma primeiro. Para registros excluídos que são fantasmas primeiro, **leaf_ghost_count** é incrementado em vez disso.|    
|**leaf_update_count**|**bigint**|Contagem cumulativa de atualizações de nível folha.|    
|**leaf_ghost_count**|**bigint**|Contagem cumulativa de linhas de nível folha marcadas como excluídas, mas não removidas ainda. Essa contagem não inclui registros que são excluídos imediatamente sem serem marcados como fantasma. Essas filas são removidas por um thread de limpeza em intervalos definidos. Esse valor não inclui linhas retidas que foram retidas, devido a uma transação de isolamento de instantâneo pendente.|    
|**nonleaf_insert_count**|**bigint**|Contagem cumulativa de inserções acima do nível folha.<br /><br /> 0 = Heap ou columnstore|    
|**nonleaf_delete_count**|**bigint**|Contagem cumulativa de exclusões acima do nível folha.<br /><br /> 0 = Heap ou columnstore|    
|**nonleaf_update_count**|**bigint**|Contagem cumulativa de atualizações acima do nível folha.<br /><br /> 0 = Heap ou columnstore|    
|**leaf_allocation_count**|**bigint**|Contagem cumulativa de alocações de página de nível folha no índice ou heap.<br /><br /> Para um índice, uma alocação de página corresponde a uma página dividida.|    
|**nonleaf_allocation_count**|**bigint**|Contagem cumulativa de alocações de página provocadas por divisões de página acima do nível folha.<br /><br /> 0 = Heap ou columnstore|    
|**leaf_page_merge_count**|**bigint**|Contagem cumulativa de mesclagens de página no nível folha. Sempre 0 para índice columnstore.|    
|**nonleaf_page_merge_count**|**bigint**|Contagem cumulativa de mesclagens de página acima do nível folha.<br /><br /> 0 = Heap ou columnstore|    
|**range_scan_count**|**bigint**|Contagem cumulativa de exames de intervalo e de tabela iniciados no índice ou heap.|    
|**singleton_lookup_count**|**bigint**|Contagem cumulativa de recuperações de linha única do índice ou heap.|    
|**forwarded_fetch_count**|**bigint**|Contagem de linhas buscadas por meio de um registro de encaminhamento.<br /><br /> 0 = Índices|    
|**lob_fetch_in_pages**|**bigint**|Contagem cumulativa de páginas de LOB (objeto grande) recuperadas da unidade de alocação LOB_DATA. Essas páginas contêm dados que são armazenados em colunas do tipo **Text**, **ntext**, **Image**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)** e **XML**. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|    
|**lob_fetch_in_bytes**|**bigint**|Contagem cumulativa de bytes de dados LOB recuperados.|    
|**lob_orphan_create_count**|**bigint**|Contagem cumulativa de valores LOB órfãos criados para operações em massa.<br /><br /> 0 = Índice não clusterizado|    
|**lob_orphan_insert_count**|**bigint**|Contagem cumulativa de valores LOB órfãos inseridos durante operações em massa.<br /><br /> 0 = Índice não clusterizado|    
|**row_overflow_fetch_in_pages**|**bigint**|Contagem cumulativa de páginas de dados de estouro de linha recuperada da unidade de alocação ROW_OVERFLOW_DATA.<br /><br /> Essas páginas contêm dados armazenados em colunas do tipo **varchar (n)**, **nvarchar (n)**, **varbinary (n)** e **sql_variant** que foram empurrados para fora da linha.|    
|**row_overflow_fetch_in_bytes**|**bigint**|Contagem cumulativa de bytes de dados de estouro de linha recuperados.|    
|**column_value_push_off_row_count**|**bigint**|Contagem cumulativa de valores de coluna para dados LOB e dados de estouro de linha empurrados para fora da linha para que uma linha atualizada ou inserida coubesse na página.|    
|**column_value_pull_in_row_count**|**bigint**|Contagem cumulativa de valores de coluna para dados de LOB e dados de estouro de linha puxados para dentro da linha. Isso ocorre quando uma operação de atualização libera espaço em um registro e fornece uma oportunidade de empurrar um ou mais valores para fora da linha das unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA.|    
|**row_lock_count**|**bigint**|Número cumulativo de bloqueios solicitados.|    
|**row_lock_wait_count**|**bigint**|Número cumulativo de vezes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou por um bloqueio de linha.|    
|**row_lock_wait_in_ms**|**bigint**|Número total de milissegundos que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou por um bloqueio de linha.|    
|**page_lock_count**|**bigint**|Número cumulativo de bloqueios de página solicitados.|    
|**page_lock_wait_count**|**bigint**|Número cumulativo de vezes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou por um bloqueio de página.|    
|**page_lock_wait_in_ms**|**bigint**|Número total de milissegundos que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou por um bloqueio de página.|    
|**index_lock_promotion_attempt_count**|**bigint**|Número cumulativo de vezes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou escalar bloqueios.|    
|**index_lock_promotion_count**|**bigint**|Número cumulativo de vezes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] escalou bloqueios.|    
|**page_latch_wait_count**|**bigint**|Número cumulativo de vezes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou devido a uma contenção de travamento.|    
|**page_latch_wait_in_ms**|**bigint**|Número cumulativo de milissegundos que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou devido a uma contenção de travamento.|    
|**page_io_latch_wait_count**|**bigint**|Número cumulativo de vezes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou em um travamento de página de E/S.|    
|**page_io_latch_wait_in_ms**|**bigint**|Número cumulativo de milissegundos que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esperou em uma trava de E/S de página.|    
|**tree_page_latch_wait_count**|**bigint**|Subconjunto de **page_latch_wait_count** que inclui apenas as páginas da árvore B de nível superior. Sempre 0 para heaps ou índices columnstore.|    
|**tree_page_latch_wait_in_ms**|**bigint**|Subconjunto de **page_latch_wait_in_ms** que inclui apenas as páginas da árvore B de nível superior. Sempre 0 para heaps ou índices columnstore.|    
|**tree_page_io_latch_wait_count**|**bigint**|Subconjunto de **page_io_latch_wait_count** que inclui apenas as páginas da árvore B de nível superior. Sempre 0 para heaps ou índices columnstore.|    
|**tree_page_io_latch_wait_in_ms**|**bigint**|Subconjunto de **page_io_latch_wait_in_ms** que inclui apenas as páginas da árvore B de nível superior. Sempre 0 para heaps ou índices columnstore.|    
|**page_compression_attempt_count**|**bigint**|Número de páginas avaliadas por compactação de nível de PAGE para partições específicas de tabela, índice ou exibição indexada. Inclui páginas que não foram compactadas porque economias significativas não puderam ser obtidas. Sempre 0 para índice columnstore.|    
|**page_compression_success_count**|**bigint**|Número de páginas de dados que foram compactadas com a compactação de PAGE para partições específicas de tabela, índice ou exibição indexada. Sempre 0 para índice columnstore.|    
    
## <a name="remarks"></a>Comentários    
 Esse objeto de gerenciamento dinâmico não aceita parâmetros correlacionados de `CROSS APPLY` e `OUTER APPLY` .    
    
 Você pode usar **sys.dm_db_index_operational_stats** para rastrear o período de tempo que os usuários devem aguardar para ler ou gravar em uma tabela, índice ou partição e identificar as tabelas ou índices que estão encontrando atividade de E/S significativa ou pontos de acesso.    
    
 Use as seguintes colunas para identificar áreas de contenção.    
    
 **Para analisar um padrão de acesso comum à tabela ou partição de índice**, use estas colunas:    
    
-   **leaf_insert_count**    
    
-   **leaf_delete_count**    
    
-   **leaf_update_count**    
    
-   **leaf_ghost_count**    
    
-   **range_scan_count**    
    
-   **singleton_lookup_count**    
    
 Para identificar a contenção de bloqueio e trava, use estas colunas:    
    
-   **page_latch_wait_count** e **page_latch_wait_in_ms**    
    
     Essas colunas indicam se há uma contenção de trava no índice ou heap e a importância da contenção.    
    
-   **row_lock_count** e **page_lock_count**    
    
     Essas colunas indicam quantas vezes o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou adquirir bloqueios de linha e página.    
    
-   **row_lock_wait_in_ms** e **page_lock_wait_in_ms**    
    
     Estas colunas indicam se há uma contenção de bloqueio no índice ou heap e a importância da contenção.    
    
 **Para analisar estatísticas de E/S física em uma partição de índice ou de heap**    
    
-   **page_io_latch_wait_count** e **page_io_latch_wait_in_ms**    
    
     Essas colunas indicam se foram emitidas E/S físicas para trazer as páginas de índice ou heap para a memória e quantas E/S foram emitidas.    
    
## <a name="column-remarks"></a>Comentários sobre colunas    
 Os valores em **lob_orphan_create_count** e **lob_orphan_insert_count** devem ser iguais sempre.    
    
 O valor nas colunas **lob_fetch_in_pages** e **lob_fetch_in_bytes** podem ser maiores do que zero para índices não clusterizados que contenham uma ou mais colunas LOB como colunas incluídas. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md). Do mesmo modo, o valor nas colunas **row_overflow_fetch_in_pages** e **row_overflow_fetch_in_bytes** poderão ser maiores do que 0 para índices não clusterizados se o índice contiver colunas que possam ser empurradas para fora da linha.    
    
## <a name="how-the-counters-in-the-metadata-cache-are-reset"></a>Como os contadores no cache de metadados são redefinidos    
 Os dados retornados por **sys.dm_db_index_operational_stats** só existem enquanto o objeto do cache de metadados que representa o heap ou o índice está disponível. Esses dados não são persistentes nem transacionalmente consistentes. Isso significa que você não pode usar esses contadores para determinar se um índice foi usado ou não, ou quando o índice foi usado pela última vez. Para obter informações sobre isso, consulte [sys.dm_db_index_usage_stats &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md).    
    
 Os valores de cada coluna são definidos como zero sempre que os metadados do heap ou do índice forem trazidos para o cache de metadados e as estatísticas são acumuladas até que o objeto do cache seja removido do cache de metadados. Portanto, um heap ou índice ativo provavelmente sempre terá seus metadados no cache e as contagens cumulativas poderão refletir a atividade desde que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciada pela última vez. Os metadados de um heap ou índice menos ativo são movidos para dentro e para fora do cache à medida que ele é usado. Como resultado, ele pode ou não ter valores disponíveis. Descartar um índice fará com que as estatísticas correspondentes sejam removidas da memória e não sejam mais reportadas pela função. Outras operações DDL em relação ao índice podem fazer com que o valor das estatísticas seja redefinido como zero.    
    
## <a name="using-system-functions-to-specify-parameter-values"></a>Usando funções do sistema para especificar valores de parâmetro    
 Você pode usar as [!INCLUDE[tsql](../../includes/tsql-md.md)] funções [DB_ID](../../t-sql/functions/db-id-transact-sql.md) e [object_id](../../t-sql/functions/object-id-transact-sql.md) para especificar um valor para os parâmetros *database_id* e *object_id* . No entanto, passar valores que não sejam válidos a essas funções pode causar resultados não intencionais. Sempre verifique se uma ID válida é retornada ao usar DB_ID ou OBJECT_ID. Para obter mais informações, consulte a seção comentários em [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).    
    
## <a name="permissions"></a>Permissões    
 Requer as seguintes permissões:    
    
-   `CONTROL` permissão no objeto especificado no banco de dados    
    
-   `VIEW DATABASE STATE` permissão para retornar informações sobre todos os objetos dentro do banco de dados especificado, usando o curinga do objeto @*object_id* = NULL    
    
-   `VIEW SERVER STATE` permissão para retornar informações sobre todos os bancos de dados, usando o caractere curinga @*database_id* = NULL    
    
 A concessão `VIEW DATABASE STATE` permite que todos os objetos no banco de dados sejam retornados, independentemente de qualquer permissão de controle negada em objetos específicos.    
    
 Negar `VIEW DATABASE STATE` não permite que todos os objetos no banco de dados sejam retornados, independentemente de qualquer permissão de controle concedida em objetos específicos. Além disso, quando o curinga do banco de dados `@database_id=NULL` é especificado, o banco de dados é omitido.    
    
 Para obter mais informações, consulte [funções e exibições de gerenciamento dinâmico &#40;&#41;Transact-SQL ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).    
    
## <a name="examples"></a>Exemplos    
    
### <a name="a-returning-information-for-a-specified-table"></a>a. Retornando informações de uma tabela especificada    
 O exemplo a seguir retorna informações de todos os índices e partições da tabela `Person.Address` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A execução dessa consulta exige, no mínimo, a permissão CONTROL para a tabela `Person.Address`.    
    
> [!IMPORTANT]    
> Ao usar as funções [!INCLUDE[tsql](../../includes/tsql-md.md)] DB_ID e OBJECT_ID para retornar um valor de parâmetro, sempre verifique se uma ID válida é retornada. Se o banco de dados ou nome de objeto não puder ser encontrado, por não existir ou por estar escrito incorretamente, ambas as funções retornarão NULL. A função **sys.dm_db_index_operational_stats** interpreta NULL como um valor de curinga que especifica todos os bancos de dados ou todos os objetos. Como pode se tratar de uma operação não intencional, os exemplos nesta seção demonstram a maneira segura de determinar a identificação do banco de dados e do objeto.    
    
```sql    
DECLARE @db_id int;    
DECLARE @object_id int;    
SET @db_id = DB_ID(N'AdventureWorks2012');    
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');    
IF @db_id IS NULL     
  BEGIN;    
    PRINT N'Invalid database';    
  END;    
ELSE IF @object_id IS NULL    
  BEGIN;    
    PRINT N'Invalid object';    
  END;    
ELSE    
  BEGIN;    
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);    
  END;    
GO    
```    
    
### <a name="b-returning-information-for-all-tables-and-indexes"></a>B. Retornando informações para todas as tabelas e índices    
 O exemplo a seguir retorna informações para todos os índices e tabelas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A execução dessa consulta exige a permissão VIEW SERVER STATE.    
    
```sql    
SELECT * FROM sys.dm_db_index_operational_stats( NULL, NULL, NULL, NULL);    
GO        
```    
    
## <a name="see-also"></a>Consulte Também    
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)     
 [Exibições e funções de gerenciamento dinâmico relacionadas ao índice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)     
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)     
 [&#41;&#40;Transact-SQL de sys.dm_db_index_usage_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)     
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)     
 [&#41;&#40;Transact-SQL de sys.dm_db_partition_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)     
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)     
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)    
    
