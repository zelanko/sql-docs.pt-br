---
title: "Índices columnstore – novidades | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1fe5ea05-5b19-45a4-9b7a-8ae5ca367897
caps.latest.revision: 28
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 47b0c3fc8aba635dcfd573536b770f13a40956fa
ms.openlocfilehash: 0a63e3e5641ce513e0d3c30705ac8a7523cbc053
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="columnstore-indexes---what39s-new"></a>Índices columnstore – novidades
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Resumo dos recursos de columnstore disponíveis para cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e as versões mais recentes do Azure SQL Database Premium Edition, Azure SQL Data Warehouse e Parallel Data Warehouse.  

 >[!NOTE]
 > Para o Banco de Dados SQL do Azure, índices columnstore só estão disponíveis na Edição Premium.
 
## <a name="feature-summary-for-product-releases"></a>Resumo de recursos para versões do produto  
 Esta tabela resume os principais recursos para índices columnstore, e os produtos nos quais eles estão disponíveis.  

  
|Recurso do índice columnstore|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Edição Premium|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]|  
|-------------------------------|---------------------------|---------------------------|---------------------------|--------------------------------------------|-------------------------|---|  
|Execução de lote para consultas com multithread|sim|sim|sim|sim|sim|sim| 
|Execução de lote para consultas com um único thread|||sim|sim|sim|sim|  
|Opção de compactação de arquivamento.||sim|sim|sim|sim|sim|  
|Isolamento de instantâneo e isolamento de instantâneo de leitura confirmada|||sim|sim|sim|sim| 
|Especificação do índice columnstore durante a criação de uma tabela.|||sim|sim|sim|sim|  
|Suporte a índices columnstore pelo AlwaysOn.|sim|sim|sim|sim|sim|sim| 
|Suporte ao índice columnstore não clusterizado somente leitura pelo secundário legível AlwaysOn|sim|sim|sim|sim|sim|sim|  
|Suporte ao índice columnstore atualizável pelo secundário legível AlwaysOn|||sim|sim|||  
|Índice columnstore não clusterizado somente leitura no heap ou árvore b.|sim|sim|sim*|sim*|sim*|sim*|  
|Índice columnstore não clusterizado atualizável no heap ou árvore b|||sim|sim|sim|sim|  
|Índices adicionais de árvore b permitidos em um heap ou árvore b com um índice columnstore não clusterizado.|sim|sim|sim|sim|sim|sim|  
|Índice columnstore clusterizado e atualizável.||sim|sim|sim|sim|sim|  
|Índice de árvore b em um índice columnstore clusterizado|||sim|sim|sim|sim|  
|Índice columnstore em uma tabela com otimização de memória.|||sim|sim|sim|sim|  
|Suporte ao uso de uma condição filtrada pela definição de índice columnstore não clusterizado.|||sim|sim|sim|sim|  
|Opção de atraso de compactação para índices columnstore em CREATE TABLE e ALTER TABLE.|||sim|sim|sim|sim|
|O índice ColumnStore pode ter uma coluna computada não persistente.||||sim|||   
  
 * Para criar um índice columnstore não clusterizado legível, armazene o índice em um grupo de arquivos somente leitura.  

## [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 
 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] adiciona esses novos recursos.

### <a name="functional"></a>Funcional
- [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] dá suporte a colunas computadas não persistentes em índices columnstore clusterizados. Não há suporte para colunas persistentes em índices columnstore clusterizados. Você não pode criar um índice não clusterizado em um índice columnstore que tenha uma coluna computada. 

## [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 O[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] adiciona aprimoramentos importantes para melhorar o desempenho e a flexibilidade dos índices columnstore. Esses aprimoramentos melhoram os cenários de data warehouse e habilitam a análise operacional em tempo real.  
  
### <a name="functional"></a>Funcional  
  
-   Uma tabela rowstore pode ter um índice columnstore não clusterizado atualizável. Anteriormente, o índice columnstore não clusterizado era somente leitura.  
  
-   A definição do índice columnstore não clusterizado oferece suporte ao uso de uma condição filtrada. Para minimizar o impacto no desempenho da adição de um índice columnstore em uma tabela OLTP, use uma condição filtrada para criar um índice columnstore não clusterizado apenas nos dados inativos da sua carga de trabalho operacional. 
  
-   Uma tabela na memória pode ter um índice columnstore. Você pode criá-lo quando a tabela for criada ou adicioná-lo mais tarde com [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md). Anteriormente, somente uma tabela baseada em disco podia ter um índice columnstore.  
  
-   Um índice columnstore clusterizado pode ter um ou mais índices rowstore não clusterizados. Anteriormente, o índice columnstore não oferecia suporte a índices não clusterizados. O SQL Server mantém automaticamente os índices não clusterizados para operações de DML.  
  
-   Ofereça suporte a chaves primárias e chaves estrangeiras usando um índice de árvore b a fim de impor essas restrições em um índice columnstore clusterizado.  
  
-   Os índices columnstore têm uma opção de atraso de compactação que minimiza o impacto da carga de trabalho transacional na análise operacional em tempo real.  Essa opção permite que as linhas alteradas frequentemente estabilizem antes de compactá-las no columnstore. Para obter detalhes, consulte [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) e [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
### <a name="performance-for-database-compatibility-level-120-or-130"></a>Desempenho do nível de compatibilidade do banco de dados 120 ou 130  
  
-   Os índices columnstore oferecem suporte ao nível RCSI (isolamento do instantâneo confirmado) e ao SI (isolamento de instantâneo). Isso permite consultas de análise consistente transacionais sem qualquer bloqueio.  
  
-   O columnstore oferece suporte à desfragmentação de índice por meio da remoção de linhas excluídas, sem a necessidade de recriar explicitamente o índice. A instrução ALTER INDEX … A instrução REORGANIZE remove do columnstore as linhas excluídas, com base em uma política definida internamente, como uma operação online  
  
-   Os índices columnstore podem ser acessados em uma réplica secundária legível do AlwaysOn. Você pode melhorar o desempenho da análise operacional descarregando as consultas de análise para uma réplica secundária do AlwaysOn.  
  
-   Para melhorar o desempenho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computa as funções de agregação MIN, MAX, SUM, COUNT, AVG durante as verificações de tabela, quando o tipo de dados usa no máximo 8 bytes e não é do tipo cadeia de caracteres. Há suporte para aplicação agregada com ou sem a cláusula Group By tanto para índices columnstore clusterizados quanto para índices columnstore não clusterizados.  
  
-   A aplicação de predicado acelera as consultas que comparam cadeias de caracteres do tipo [v]char ou n[v]char. Isso se aplica aos operadores de comparação comuns e inclui operadores como LIKE, que usam filtros de bitmap. Isso funciona com todos os agrupamentos com suporte do SQL Server.  
  
### <a name="performance-for-database-compatibility-level-130"></a>Desempenho do nível de compatibilidade do banco de dados 130  
  
-   Novo suporte à execução em modo de lote para consultas que usam qualquer uma dessas operações:  
  
    -   SORT  
  
    -   Realiza agregações com várias funções diferentes. Alguns exemplos: COUNT/COUNT, AVG/SUM, CHECKSUM_AGG, STDEV/STDEVP.  
  
    -   Funções de agregação de janela: COUNT, COUNT_BIG, SUM, AVG, MIN, MAX e CLR.  
  
    -   Agregações de janela definidas pelo usuário: CHECKSUM_AGG, STDEV, STDEVP, VAR, VARP e GROUPING.  
  
    -   Funções de análise de agregação de janela:  LAG< LEAD, FIRST_VALUE, LAST_VALUE, PERCENTILE_CONT, PERCENTILE_DISC, CUME_DIST e PERCENT_RANK.  
  
-   Consultas de thread único em execução no MAXDOP 1, ou com um plano de consulta em série, executam no modo de lote. Anteriormente, somente consultas multithread executavam com a execução de lote.  
  
-   Consultas de tabela com otimização de memória podem ter planos paralelos no modo de interoperabilidade de SQL ao acessar dados em rowstore ou no índice columnstore  
  
### <a name="supportability"></a>Suporte  
 Esses modos de exibição do sistema são novos no columnstore:  
  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  
  
-   [sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)  
  
 Esses DMVs baseados em OLTP na memória contêm atualizações para o columnstore:  
  
-   [sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)  
  
-   [sys.dm_db_xtp_nonclustered_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_object_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)  
  
### <a name="limitations"></a>Limitações  
  
-   MERGE é desabilitado quando um índice de árvore b é definido em um índice columnstore clusterizado.  
  
-   Para tabelas na memória, um índice columnstore deve incluir todas as colunas; o índice columnstore não pode ter uma condição filtrada.  
  
-   Para tabelas na memória, as consultas em índices columnstore são executadas somente no modo de interoperabilidade, e não no modo nativo na memória. Há suporte para a execução paralela.  
  
## <a name="sql-server-2014"></a>SQL Server 2014  
 O SQL Server 2014 introduziu o índice de repositório de coluna clusterizado como o formato de armazenamento principal. Isso permitiu cargas regulares, bem como operações de atualização, exclusão e inserção.  
  
-   A tabela pode usar um índice de repositório de coluna clusterizado como o armazenamento de tabela primária. Nenhum outro índice tem permissão na tabela, mas o índice de repositório de coluna clusterizado é atualizável, de modo que você possa executar cargas regulares e fazer alterações em linhas individuais.  
  
-   O índice de repositório de coluna não clusterizado continua com a mesma funcionalidade que tinha no SQL Server 2012, exceto no caso de operadores adicionais que, agora, podem ser executados em modo de lote. Ainda não é atualizável, exceto por meio de recompilação e usando a alternância de partição. O índice columnstore não clusterizado tem suporte apenas em tabelas baseadas em disco, e não em tabelas na memória.  
  
-   O índice de repositório de coluna clusterizado e não clusterizado tem uma opção de compactação de arquivamento que compacta ainda mais os dados. A opção de arquivamento é útil para reduzir o tamanho dos dados na memória e no disco, mas também reduz o desempenho da consulta. Ela funciona bem para dados acessados com pouca frequência.  
  
-   O índice columnstore clusterizado e o índice columnstore não clusterizado funcionam de modo muito semelhante; eles usam o mesmo formato de armazenamento colunar, o mesmo mecanismo de processamento de consulta e o mesmo conjunto de exibições de gerenciamento dinâmico. A diferença é de tipos de índice primário e secundário, e o índice columnstore não clusterizado é somente leitura.  
  
-   Estes operadores são executados em modo de lote para consultas multithread: verificação, filtro, projeto, união, agrupar por e união de todos.  
  
## <a name="sql-server-2012"></a>SQL Server 2012  
 O SQL Server 2012 introduziu o índice columnstore não clusterizado como outro tipo de índice em tabelas rowstore e processamento em lote para consultas em dados de columnstore.  
  
-   Uma tabela rowstore pode ter um índice columnstore não clusterizado.  
  
-   O índice columnstore é somente leitura. Depois de criar o índice columnstore, você não pode atualizar a tabela com operações de inserção, exclusão e atualização; para executar essas operações é necessário descartar o índice, atualizar a tabela e recompilar o índice columnstore. Você pode carregar dados adicionais na tabela usando a alternância de partição. A vantagem da alternância de partição é que você pode carregar dados sem descartar e recompilar o índice columnstore.  
  
-   O índice de repositório de coluna sempre exige armazenamento extra, normalmente 10% a mais no rowstore, pois ele armazena uma cópia dos dados.  
  
-   O processamento de lote fornece um desempenho de consulta duas ou mais vezes melhor, mas está disponível apenas para execução de consulta paralela.  
  
## <a name="see-also"></a>Consulte também  
 Guia de Índices columnstore   
 Carregamento de dados dos Índices columnstore   
 [Desempenho de consultas de índices ColumnStore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 Índices columnstore para Data Warehousing   
 [Desfragmentação de índices columnstore](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  

