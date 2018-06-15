---
title: Índices columnstore – visão geral | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
caps.latest.revision: 80
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1987c099ba787f36dac77eb08a8e88b1e7c71869
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32941011"
---
# <a name="columnstore-indexes---overview"></a>Índices columnstore – visão geral
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Os *índices columnstore* são o padrão para armazenar e consultar tabelas de fatos com armazenamento de dados grandes. Ele usa armazenamento de dados baseado em coluna e processamento de consultas para alcançar um **desempenho de consulta até 10 vezes melhor** no data warehouse em relação ao armazenamento tradicional orientado por linha e até **10 vezes mais compactação de dados** em relação ao tamanho dos dados descompactados. A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], os índices columnstore permitem a análise operacional, a capacidade de executar análises de alto desempenho em tempo real em uma carga de trabalho transacional.  
  
 Passar para cenários:  
  
-   [Índices columnstore para Data Warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
-   [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
## <a name="what-is-a-columnstore-index"></a>O que é um índice columnstore?  
 Um *columnstore index* é uma tecnologia para armazenamento, recuperação e gerenciamento de dados usando um formato de dados colunar, chamado columnstore.  
  
### <a name="key-terms-and-concepts"></a>Termos e conceitos essenciais  
 Os termos e conceitos essenciais a seguir estão associados aos índices columnstore.  
  
 columnstore  
 Um *columnstore* são dados logicamente organizados como uma tabela com linhas e colunas e fisicamente armazenados em um formato de dados com reconhecimento de coluna.  
  
 rowstore  
 Um *rowstore* são dados logicamente organizados como uma tabela com linhas e colunas e fisicamente armazenados em um formato de dados com reconhecimento de linha. Esse tem sido o modo tradicional de armazenar dados da tabela relacional. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], rowstore refere-se à tabela em que o formato de armazenamento de dados subjacente é um heap, um índice clusterizado ou uma tabela com otimização de memória.  
  
> [!NOTE]  
> Em discussões sobre índices columnstore, usamos os termos *rowstore* e *columnstore* para enfatizar o formato do armazenamento de dados.  
  
 rowgroup  
 Um *row group* é um grupo de linhas que são compactadas no formato columnstore ao mesmo tempo. Um grupo de linhas normalmente contém o número máximo de linhas por grupo de linhas que é 1.048.576 linhas.  
  
 Para altas taxas de desempenho e compactação, o índice columnstore fatia a tabela em grupos de linhas, chamados de rowgroups, e depois compacta cada um desses grupos com um método com reconhecimento de coluna. O número de linhas no rowgroup deve ser grande o suficiente para melhorar as taxas de compactação e pequeno o suficiente para se beneficiar com as operações na memória.  
 segmento de coluna  
 Um *segmento de coluna* é uma coluna de dados do grupo de linhas.  
  
-   Cada rowgroup contém um segmento de coluna para cada coluna na tabela.  
-   Cada segmento de coluna é compactado junto e armazenado em meio físico.  
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
  
 índice columnstore clusterizado  
 Um *índice columnstore clusterizado* é o armazenamento físico da tabela inteira.  
  
 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")  
  
 Para reduzir a fragmentação dos segmentos de coluna e melhorar o desempenho, o índice columnstore pode armazenar alguns dados temporariamente em um índice clusterizado, chamado deltastore, e em uma lista árvore B de IDs para linhas excluídas. As operações de deltastore são tratadas em segundo plano. Para retornar os resultados corretos da consulta, o índice columnstore clusterizado combina os resultados da consulta de columnstore e deltastore.  
  
 rowgroup delta  
 Usado somente com índices de repositório de colunas, um *rowgroup delta* é um índice clusterizado que melhora o desempenho e a compactação do columnstore armazenando linhas até que o número de linhas alcance um limite e seja, em seguida, movido para o columnstore.  

 Quando um rowgroup delta alcança o número máximo de linhas, ele fica fechado. Um processo de movimentação de tupla procura grupos de linhas fechados. Quando encontra o grupo de linhas fechado, compacta-o e armazena-o no columnstore.  
  
Um índice columnstore deltastore A pode ter mais de um rowgroup delta.  Todos os rowgroups delta são coletivamente chamados de *deltastore*.   

Durante o carregamento em massa grande, a maioria das linhas vai diretamente para o columnstore sem passar pelo deltastore. No fim do carregamento em massa, o número de linhas pode ser muito pouco para atender ao tamanho mínimo de um rowgroup, que é de 102.400 linhas. Quando isso ocorre, as linhas finais vão para o deltastore, e não para o columnstore. Para carregamento em massa pequeno, menos de 102.400 linhas, todas as linhas vão diretamente para o deltastore.  
  

  
 índice columnstore não clusterizado  
 Um *índice columnstore não clusterizado* e um índice columnstore clusterizado funcionam da mesma maneira. A diferença é que um índice não clusterizado é um índice secundário criado em uma tabela rowstore, enquanto um índice columnstore clusterizado é o armazenamento primário da tabela inteira.  
  
 O índice não clusterizado contém uma cópia de parte ou de todas as linhas e colunas na tabela subjacente. O índice é definido como uma ou mais colunas da tabela e tem uma condição opcional que filtra as linhas.  
  
 Um índice não clusterizado columnstore permite análises operacionais em tempo real nas quais a carga de trabalho OLTP usa o índice clusterizado subjacente, enquanto as análises são executadas simultaneamente no índice columnstore. Para obter mais informações, veja [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
 execução em lote  
 *Execução em lote* é um método no qual as consultas processam várias linhas simultaneamente. Consultas em índices columnstore usam a execução em modo de lote, o que melhora o desempenho de consulta normalmente em 2 a 4 vezes. A execução em lote é integrada ao formato de armazenamento columnstore e otimizada com base nele. A execução do modo em lote às vezes é conhecida como execução baseada em vetor ou vetorizado.  
  
##  <a name="benefits"></a> Por que devo usar um índice columnstore?  
 Um índice columnstore pode fornecer um nível muito alto de compactação de dados, geralmente de 10 vezes, para reduzir significativamente os custos de armazenamento em data warehouse. Além disso, para análises, esses índices oferecem um desempenho melhor de ordem de magnitude do que um índice de árvore B. Eles são o formato de armazenamento de dados preferencial para data warehouse e cargas de trabalho de análise. A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode usar índices columnstore para análises em tempo real da sua carga de trabalho operacional.  
  
 Motivos pelos quais índices columnstore são tão rápidos:  
  
-   Colunas armazenam valores do mesmo domínio e normalmente têm valores semelhantes, o que resulta em altas taxas de compactação. Isso minimiza ou elimina os gargalos de E/S no seu sistema e reduz a ocupação da memória de forma significativa.  
  
-   As altas taxas de compactação melhoram o desempenho da consulta usando um menor volume na memória. Por sua vez, o desempenho da consulta pode ser melhorado porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode realizar mais operações de consulta e dados na memória.  
  
-   A execução em lote melhora o desempenho de consulta, normalmente em 2 a 4 vezes, processando várias linhas simultaneamente.  
  
-   Muitas vezes, as consultas selecionam apenas algumas colunas de uma tabela, o que reduz a E/S total da mídia física.  
  
## <a name="when-should-i-use-a-columnstore-index"></a>Quando devo usar um índice columnstore?  
 Casos de uso recomendados:  
  
-   Use um índice columnstore clusterizado para armazenar tabelas de fatos e tabelas de dimensões grandes para cargas de trabalho de data warehouse. Isso melhora o desempenho de consulta e a compactação de dados em até 10 vezes. Consulte [Columnstore Indexes for Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md).  
  
-   Use um índice columnstore não clusterizado para executar análises em tempo real em uma carga de trabalho OLTP. Veja [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
### <a name="how-do-i-choose-between-a-rowstore-index-and-a-columnstore-index"></a>Como escolher entre um índice rowstore e um índice columnstore?  
 Índices rowstore têm melhor desempenho em consultas que buscam nos dados, procurando um valor específico, ou para consultas em um pequeno intervalo de valores. Use índices rowstore com cargas de trabalho transacionais, pois eles tendem a exigir principalmente buscas de tabela em vez de verificações de tabela.  
  
 Os índices columnstore oferecem altos ganhos de desempenho para consultas analíticas que examinam grandes quantidades de dados, especialmente em tabelas grandes.  Use índices columnstore em cargas de trabalho de data warehouse e análise, especialmente em tabelas de fatos, pois eles tendem a exigir verificações de tabela completas em vez de buscas de tabela.  
  
### <a name="can-i-combine-rowstore-and-columnstore-on-the-same-table"></a>Posso combinar rowstore e columnstore na mesma tabela?  
 Sim. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar um índice columnstore não clusterizado atualizável em uma tabela rowstore. O índice columnstore armazena uma cópia das colunas escolhidas, então você precisa de espaço adicional, mas ela será compactada em 10 vezes, em média. Com isso, você pode executar análises no índice columnstore e transações no índice rowstore ao mesmo tempo. O repositório de colunas é atualizado quando dados são alterados na tabela rowstore, assim, ambos os índices trabalham com os mesmos dados.  
  
 Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode ter um ou mais índices rowstore não clusterizados em um índice columnstore. Fazendo isso, você pode executar buscas de tabela eficientes no columnstore subjacente. Outras opções também são disponibilizadas. Por exemplo, você pode impor uma restrição de chave primária usando uma restrição UNIQUE na tabela rowstore. Como um valor não exclusivo não poderá ser inserido na tabela rowstore, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá inserir o valor no columnstore.  
  
## <a name="metadata"></a>Metadados  
 Todas as colunas em um índice columnstore são armazenadas nos metadados como colunas incluídas. O índice columnstore não tem colunas de chave.  

|||
|-|-|  
|[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)|[sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)|  
|[sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)|[sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)|  
|[sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)|[sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)|  
|[sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)|[sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)|[sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)|  
|[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)||  
  
## <a name="related-tasks"></a>Related Tasks  
 Todas as tabelas relacionais usam rowstore como formato de dados subjacente, a menos que você as especifique como um índice columnstore clusterizado. `CREATE TABLE` cria uma tabela rowstore, a menos que a opção `WITH CLUSTERED COLUMNSTORE INDEX` seja especificada.  
  
 Ao criar uma tabela com a instrução `CREATE TABLE`, você pode criar a tabela como um columnstore especificando a opção `WITH CLUSTERED COLUMNSTORE INDEX`. Caso já tenha uma tabela rowstore e deseje convertê-la em um columnstore, use a instrução `CREATE COLUMNSTORE INDEX`.  
  
|Tarefa|Tópicos de referência|Observações|  
|----------|----------------------|-----------|  
|Crie uma tabela como columnstore.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar a tabela como um índice columnstore clusterizado. Não é preciso criar primeiro uma tabela rowstore e convertê-la em columnstore.|  
|Crie uma tabela de memória com um índice columnstore.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar uma tabela com otimização na memória com um índice columnstore. O índice columnstore também pode ser adicionado após a criação da tabela, usando a sintaxe ALTER TABLE ADD INDEX.|  
|Converta uma tabela rowstore em columnstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Converta uma pilha ou árvore binária existente em columnstore. Exemplos mostram como lidar com os índices existentes e o nome do índice ao realizar essa conversão.|  
|Converta uma tabela columnstore em rowstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Geralmente, isso não é necessário, mas pode haver ocasiões em que você precisa para realizar essa conversão. Exemplos mostram como converter um columnstore em uma pilha ou um índice clusterizado.|  
|Crie um índice columnstore em uma tabela rowstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Uma tabela rowstore pode ter um índice columnstore.  Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o índice columnstore pode ter uma condição filtrada. Exemplos mostram a sintaxe básica.|  
|Crie índices de alto desempenho para análises operacionais.|[Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|Descreve como criar índices de árvore B e columnstore complementares para que consultas OLTP usem índices de árvore B e consultas de análise usem índices columnstore.|  
|Crie índices columnstore de alto desempenho para data warehouse.|[Índices columnstore para Data Warehouse](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Descreve como usar índices de árvore B em tabelas columnstore para criar consultas de data warehouse de alto desempenho.|  
|Use um índice de árvore B para impor uma restrição de chave primária em um índice columnstore.|[Índices columnstore para Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Mostra como combinar índices columnstore e de árvore B para impor restrições de chave primária no índice columnstore.|  
|Remover um índice columnstore|[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)|A remoção de um índice columnstore usa a sintaxe DROP INDEX padrão usada pelos índices de árvore B. Remover um índice columnstore clusterizado converterá a tabela columnstore em uma pilha.|  
|Excluir uma linha de um índice columnstore|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Use [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) para excluir uma linha.<br /><br /> **linha columnstore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca a linha como excluída logicamente, mas não recupera o armazenamento físico da linha até que o índice seja recriado.<br /><br /> **linha deltastore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui a linha lógica e fisicamente.|  
|Atualizar uma linha no índice columnstore|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|Use [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) para atualizar uma linha.<br /><br /> **linha columnstore** :  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca a linha como excluída logicamente e insere a linha atualizada no deltastore.<br /><br /> **linha deltastore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualiza a linha no deltastore.|  
|Carregar dados em um índice columnstore|[Carregamento de dados dos índices columnstore](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)||  
|Força todas as linhas no deltastore a ir para o columnstore.|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) ... REBUILD<br /><br /> [Desfragmentação de índices columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)|ALTER INDEX com a opção REBUILD força todas as linhas a ir para o columnstore.|  
|Desfragmentar um índice columnstore|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)|ALTER INDEX … REORGANIZE desfragmenta os índices columnstore online.|  
|Mescle tabelas com índices columnstore.|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)||  
  
## <a name="see-also"></a>Consulte Também  
 [Carregamento de dados dos índices columnstore](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Resumo de recursos com versão dos índices columnstore](~/relational-databases/indexes/columnstore-indexes-what-s-new.md)   
 [Desempenho de consultas de índices ColumnStore](~/relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Índices columnstore para Data Warehouse](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Desfragmentação de índices columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)   
 [Guia de criação de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md)   
 [Arquitetura de índices columnstore](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)   
  
  





