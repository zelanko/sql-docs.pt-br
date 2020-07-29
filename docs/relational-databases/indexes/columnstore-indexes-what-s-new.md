---
title: Índices columnstore – novidades | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e60e549a83440338eaef2624761af3b9cf2426f8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246245"
---
# <a name="columnstore-indexes---what39s-new"></a>Índices columnstore – novidades
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Resumo de recursos columnstore disponíveis para cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e para as versões mais recentes do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  

 > [!NOTE]
 > No [!INCLUDE[ssSDS](../../includes/sssds-md.md)], os índices columnstore estão disponíveis nas camadas Premium e Standard do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] – S3 e superior, e em todas as camadas de vCore. Para o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 e posterior, índices columnstore estão disponíveis em todas as edições. Para o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (anterior ao SP1) e versões mais antigas, os índices columnstore estão disponíveis apenas na Enterprise Edition.
 
## <a name="feature-summary-for-product-releases"></a>Resumo de recursos para versões do produto  
 Esta tabela resume os principais recursos para índices columnstore, e os produtos nos quais eles estão disponíveis.  

|Recurso do índice columnstore|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]|  
|-------------------------------|---------------------------|---------------------------|---------------------------|--------------------------------------------|-------------------------|---|  
|Execução em modo de lote para consultas com multithread|sim|sim|sim|sim|sim|sim| 
|Execução em modo de lote para consultas com thread único|||sim|sim|sim|sim|  
|Opção de compactação de arquivamento||sim|sim|sim|sim|sim|  
|Isolamento de instantâneo e isolamento de instantâneo de leitura confirmada|||sim|sim|sim|sim| 
|Especificação do índice columnstore durante a criação de uma tabela|||sim|sim|sim|sim|  
|Suporte a índices columnstore pelo Always On|sim|sim|sim|sim|sim|sim| 
|Suporte ao índice columnstore não clusterizado somente leitura pelo secundário legível Always On|sim|sim|sim|sim|sim|sim|  
|Suporte ao índice columnstore atualizável pelo secundário legível Always On|||sim|sim|||  
|Índice columnstore não clusterizado somente leitura no heap ou árvore B|sim|sim|sim <sup>1</sup>|sim <sup>1</sup>|sim <sup>1</sup>|sim <sup>1</sup>|  
|Índice columnstore não clusterizado atualizável no heap ou árvore B|||sim|sim|sim|sim|  
|Índices adicionais de árvore B permitidos em um heap ou árvore B com um índice columnstore não clusterizado|sim|sim|sim|sim|sim|sim|  
|Índice columnstore clusterizado e atualizável||sim|sim|sim|sim|sim|  
|Índice de árvore B em um índice columnstore clusterizado|||sim|sim|sim|sim|  
|Índice columnstore em uma tabela com otimização de memória|||sim|sim|sim|sim|  
|Suporte ao uso de uma condição filtrada pela definição de índice columnstore não clusterizado|||sim|sim|sim|sim|  
|Opção de atraso de compactação para índices columnstore em `CREATE TABLE` e `ALTER TABLE`|||sim|sim|sim|sim|
|O índice columnstore pode ter uma coluna computada não persistente||||sim|||   
  
 <sup>1</sup> Para criar um índice columnstore não clusterizado somente leitura, armazene o índice em um grupo de arquivos somente leitura.  
 
> [!NOTE]
> O DOP (grau de paralelismo) para operações no [modo de lote](../../relational-databases/query-processing-architecture-guide.md#batch-mode-execution) é limitado a 2 para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Edição Standard e a 1 para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Edições Web e Express. Refere-se a índices de columnstore criados em tabelas baseadas em disco e tabelas com otimização de memória.

## [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 
 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] adiciona esses novos recursos.

### <a name="functional"></a>Funcional
- A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], o motor de tupla recebe a ajuda de uma tarefa de mesclagem em segundo plano que compacta automaticamente os rowGroups OPEN delta menores que existiram por algum tempo, conforme determinado por um limite interno, ou mescla os rowGroups COMPACTADOS dos quais foi excluído um grande número de linhas. Anteriormente, era necessária uma operação de reorganização de índice para mesclar rowgroups com dados parcialmente excluídos. Isso melhora a qualidade do índice columnstore ao longo do tempo. 

## [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 
 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] adiciona esses novos recursos.

### <a name="functional"></a>Funcional
- [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] dá suporte a colunas computadas não persistentes em índices columnstore clusterizados. Não há suporte para colunas computadas em índices columnstore clusterizados. Você não pode criar um índice não clusterizado em um índice columnstore que tenha uma coluna computada. 

## [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 O[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] adiciona aprimoramentos importantes para melhorar o desempenho e a flexibilidade dos índices columnstore. Esses aprimoramentos melhoram os cenários de data warehouse e habilitam a análise operacional em tempo real.  
  
### <a name="functional"></a>Funcional  
  
-   Uma tabela rowstore pode ter um índice columnstore não clusterizado atualizável. Anteriormente, o índice columnstore não clusterizado era somente leitura.  
  
-   A definição do índice columnstore não clusterizado oferece suporte ao uso de uma condição filtrada. Para minimizar o impacto no desempenho da adição de um índice columnstore em uma tabela OLTP, use uma condição filtrada para criar um índice columnstore não clusterizado apenas nos dados inativos da sua carga de trabalho operacional. 
  
-   Uma tabela na memória pode ter um índice columnstore. Você pode criá-lo quando a tabela for criada ou adicioná-lo mais tarde com [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md). Anteriormente, somente uma tabela baseada em disco podia ter um índice columnstore.  
  
-   Um índice columnstore clusterizado pode ter um ou mais índices rowstore não clusterizados. Anteriormente, o índice columnstore não oferecia suporte a índices não clusterizados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém automaticamente os índices não clusterizados para operações de DML.  
  
-   Dê suporte a chaves primárias e chaves estrangeiras usando um índice de árvore B para impor essas restrições em um índice columnstore clusterizado.  
  
-   Os índices columnstore têm uma opção de atraso de compactação que minimiza o impacto da carga de trabalho transacional na análise operacional em tempo real.  Essa opção permite que as linhas alteradas frequentemente estabilizem antes de compactá-las no columnstore. Para obter detalhes, consulte [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) e [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
### <a name="performance-for-database-compatibility-level-120-or-130"></a>Desempenho do nível de compatibilidade do banco de dados 120 ou 130  
  
-   Os índices columnstore oferecem suporte ao nível RCSI (isolamento do instantâneo confirmado) e ao SI (isolamento de instantâneo). Isso permite consultas de análise consistente transacionais sem qualquer bloqueio.  
  
-   O columnstore oferece suporte à desfragmentação de índice por meio da remoção de linhas excluídas, sem a necessidade de recriar explicitamente o índice. A instrução `ALTER INDEX ... REORGANIZE` remove do columnstore as linhas excluídas, com base em uma política definida internamente, como uma operação online  
  
-   Os índices columnstore podem ser acessados em uma réplica secundária para leitura do AlwaysOn. Você pode melhorar o desempenho da análise operacional descarregando as consultas de análise para uma réplica secundária Always On.  
  
-   A aplicação agregada calcula as funções de agregação `MIN`, `MAX`, `SUM`, `COUNT` e `AVG` durante as verificações de tabela, quando o tipo de dados usa, no máximo, 8 bytes e não é do tipo de dados String. A aplicação agregada é compatível com ou sem a cláusula `GROUP BY` tanto para índices columnstore clusterizados quanto para índices columnstore não clusterizados. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa melhoria é reservada para a edição Enterprise.
  
-   A aplicação de predicado de cadeia de caracteres acelera as consultas que comparam cadeias de caracteres do tipo VARCHAR/CHAR ou NVARCHAR/NCHAR. Isso se aplica aos operadores de comparação comuns e inclui operadores como `LIKE`, que usam filtros de bitmap. Isso funciona com todos os agrupamentos compatíveis. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa melhoria é reservada para a Edição Enterprise. 

-   Aprimoramentos para operações do modo de lote aproveitando os recursos de hardware baseados em vetor. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta o nível de suporte de CPU para extensões de hardware AVX 2 (extensões de vetor avançadas) e SSE 4 (Extensões SIMD de Streaming 4) e as usa, se compatíveis. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa melhoria é reservada para a edição Enterprise.
  
### <a name="performance-for-database-compatibility-level-130"></a>Desempenho do nível de compatibilidade do banco de dados 130  
  
-   Novo suporte à execução em modo de lote para consultas que usam qualquer uma dessas operações:  
    -   `SORT`  
    -   Realiza agregações com várias funções diferentes. Alguns exemplos: `COUNT/COUNT`, `AVG/SUM`, `CHECKSUM_AGG` e `STDEV/STDEVP`  
    -   Funções de agregação de janela: `COUNT`, `COUNT_BIG`, `SUM`, `AVG`, `MIN`, `MAX` e `CLR`  
    -   Agregações de janela definidas pelo usuário: `CHECKSUM_AGG`, `STDEV`, `STDEVP`, `VAR`, `VARP` e `GROUPING`  
    -   Funções analíticas de agregação de janela: `LAG`, `LEAD`, `FIRST_VALUE`, `LAST_VALUE`, `PERCENTILE_CONT`, `PERCENTILE_DISC`, `CUME_DIST` e `PERCENT_RANK`  

-   Consultas single-threaded em execução em `MAXDOP 1` ou com um plano de consulta serial são executadas no modo de lote. Anteriormente, somente consultas multithread executavam com a execução de lote.  

-   Consultas de tabela com otimização de memória podem ter planos paralelos no modo de interoperabilidade de SQL ao acessar dados em rowstore ou no índice columnstore.
  
### <a name="supportability"></a>Suporte  
Esses modos de exibição do sistema são novos no columnstore:  
  
:::row:::
    :::column:::
        [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  
Esses DMVs baseados em OLTP na memória contêm atualizações para o columnstore:  

:::row:::
    :::column:::
        [sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_db_xtp_nonclustered_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sys.dm_db_xtp_object_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="limitations"></a>Limitações    
-   Para tabelas na memória, um índice columnstore deve incluir todas as colunas; o índice columnstore não pode ter uma condição filtrada.  
-   Para tabelas na memória, as consultas em índices columnstore são executadas somente no modo de interoperabilidade, e não no modo nativo na memória. Há suporte para a execução paralela.  
  
## [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] introduziu o índice de columnstore clusterizado como o formato de armazenamento primário. Isso permitiu cargas regulares, bem como operações de atualização, exclusão e inserção.  
  
-   A tabela pode usar um índice de repositório de coluna clusterizado como o armazenamento de tabela primária. Nenhum outro índice tem permissão na tabela, mas o índice de repositório de coluna clusterizado é atualizável, de modo que você possa executar cargas regulares e fazer alterações em linhas individuais.  
-   O índice de columnstore não clusterizado continua tendo a mesma funcionalidade que tinha no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], exceto no caso de operadores adicionais que, agora, podem ser executados no modo de lote. Ainda não é atualizável, exceto por meio de recompilação e usando a alternância de partição. O índice columnstore não clusterizado tem suporte apenas em tabelas baseadas em disco, e não em tabelas na memória.  
-   O índice de repositório de coluna clusterizado e não clusterizado tem uma opção de compactação de arquivamento que compacta ainda mais os dados. A opção de arquivamento é útil para reduzir o tamanho dos dados na memória e no disco, mas também reduz o desempenho da consulta. Ela funciona bem para dados acessados com pouca frequência.  
-   O índice columnstore clusterizado e o índice columnstore não clusterizado funcionam de modo muito semelhante; eles usam o mesmo formato de armazenamento colunar, o mesmo mecanismo de processamento de consulta e o mesmo conjunto de exibições de gerenciamento dinâmico. A diferença é de tipos de índice primário e secundário, e o índice columnstore não clusterizado é somente leitura.  
-   Estes operadores são executados em modo de lote para consultas multithread: verificação, filtro, projeto, união, agrupar por e união de todos.  
  
## [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
 O [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] introduziu o índice columnstore não clusterizado como outro tipo de índice em tabelas rowstore e no processamento em lotes para consultas em dados de columnstore.  
  
-   Uma tabela rowstore pode ter um índice columnstore não clusterizado.  
-   O índice columnstore é somente leitura. Depois de criar o índice columnstore, não é possível atualizar a tabela com operações `INSERT`, `DELETE` e `UPDATE`; para executar essas operações, é necessário remover o índice, atualizar a tabela e recompilar o índice columnstore. Você pode carregar dados adicionais na tabela usando a alternância de partição. A vantagem da alternância de partição é que você pode carregar dados sem descartar e recompilar o índice columnstore.  
-   O índice de repositório de coluna sempre exige armazenamento extra, normalmente 10% a mais no rowstore, pois ele armazena uma cópia dos dados.  
-   O processamento de lote fornece um desempenho de consulta duas ou mais vezes melhor, mas está disponível apenas para execução de consulta paralela.  
  
## <a name="see-also"></a>Consulte Também  
 [Diretrizes de design dos Índices columnstore](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Diretrizes de Carregamento de Dados de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Desempenho de consultas de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Índices columnstore para Data Warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)
  
