---
title: 'Índices columnstore: Visão geral | Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- batch mode execution
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d48ff63d5ea5ab7ed805eb7db092fa35682bbc9b
ms.sourcegitcommit: 594cee116fa4ee321e1f5e5206f4a94d408f1576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009402"
---
# <a name="columnstore-indexes-overview"></a>Índices columnstore: Visão geral
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Os índices columnstore são o padrão para armazenar e consultar tabelas de fatos com armazenamento de dados grandes. Esse índice usa armazenamento de dados baseado em coluna e processamento de consultas para obter até **10 vezes mais desempenho de consulta** em seu data warehouse em relação ao armazenamento tradicional orientado por linha. Também é possível obter até **10 vezes mais compactação de dados** em relação ao tamanho dos dados descompactados. A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], os índices columnstore permitem a análise operacional, a capacidade de executar análises de alto desempenho em tempo real em uma carga de trabalho transacional.  
  
Confira um cenário relacionado:  
  
-   [Índices columnstore para data warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
-   [Introdução ao columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
## <a name="what-is-a-columnstore-index"></a>O que é um índice columnstore?  
Um columnstore index é uma tecnologia para armazenamento, recuperação e gerenciamento de dados usando um formato de dados colunar, chamado *columnstore*.  
  
### <a name="key-terms-and-concepts"></a>Termos e conceitos essenciais  
Os termos e conceitos principais a seguir estão associados aos índices columnstore.  
  
#### <a name="columnstore"></a>columnstore
Um columnstore são dados logicamente organizados como uma tabela com linhas e colunas e fisicamente armazenados em um formato de dados com reconhecimento de coluna.  
  
#### <a name="rowstore"></a>Rowstore
Um rowstore são dados logicamente organizados como uma tabela com linhas e colunas e fisicamente armazenados em um formato de dados com reconhecimento de linha. Esse formato é o modo tradicional de armazenar dados da tabela relacional. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], rowstore refere-se a uma tabela em que o formato de armazenamento de dados subjacente é um heap, um índice clusterizado ou uma tabela com otimização de memória.  
  
> [!NOTE]  
> Em discussões sobre índices columnstore, os termos rowstore e columnstore são usados para enfatizar o formato do armazenamento de dados.  
  
#### <a name="rowgroup"></a>Rowgroup
Um rowgroup é um grupo de linhas que são compactadas no formato columnstore ao mesmo tempo. Um rowgroup normalmente contém o número máximo de linhas por grupo de linhas que é 1.048.576 linhas.  
  
Para taxas altas de desempenho e compactação, o índice columnstore fatia a tabela em rowgroups e depois compacta cada um desses rowgroups com um método com reconhecimento de coluna. O número de linhas no rowgroup deve ser grande o suficiente para melhorar as taxas de compactação e pequeno o suficiente para se beneficiar com as operações na memória.    

#### <a name="column-segment"></a>segmento de coluna
Um segmento de coluna é uma coluna de dados do grupo de linhas.  
  
-   Cada rowgroup contém um segmento de coluna para cada coluna na tabela.  
-   Cada segmento de coluna é compactado junto e armazenado em meio físico.  
  
![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
  
#### <a name="clustered-columnstore-index"></a>Índice columnstore clusterizado
Um índice columnstore clusterizado é o armazenamento físico da tabela inteira.    
  
![Índice Columnstore Clusterizado](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Índice Columnstore Clusterizado")  
  
Para reduzir a fragmentação dos segmentos de coluna e melhorar o desempenho, o índice columnstore pode armazenar alguns dados temporariamente em um índice clusterizado, chamado *deltastore*, e em uma lista árvore B de IDs para linhas excluídas. As operações de deltastore são tratadas em segundo plano. Para retornar os resultados corretos da consulta, o índice columnstore clusterizado combina os resultados da consulta de columnstore e deltastore.  
  
#### <a name="delta-rowgroup"></a>Rowgroup delta
Um rowgroup delta é um índice clusterizado que é usado somente com índices columnstore. Ele melhora o desempenho e a compactação do columnstore armazenando linhas até que o número de linhas alcance um limite e seja, em seguida, movido para o columnstore.  

Quando um rowgroup delta alcança o número máximo de linhas, ele fica fechado. Um processo de movimentação de tupla procura grupos de linhas fechados. Se o processo encontrar um rowgroup fechado, ele o compactará e o armazenará no columnstore.  
  
#### <a name="deltastore"></a>Deltastore
Um índice columnstore pode ter mais de um rowgroup delta. Todos os rowgroups delta são coletivamente chamados de deltastore.   

Durante o carregamento em massa grande, a maioria das linhas vai diretamente para o columnstore sem passar pelo deltastore. No fim do carregamento em massa, o número de linhas pode ser muito pouco para atender ao tamanho mínimo de um rowgroup, que é de 102.400 linhas. Como resultado, as linhas finais vão para o deltastore, e não para o columnstore. Para carregamento em massa pequeno, menos de 102.400 linhas, todas as linhas vão diretamente para o deltastore.  
  
#### <a name="nonclustered-columnstore-index"></a>índice columnstore não clusterizado
Um índice columnstore não clusterizado e um índice columnstore clusterizado funcionam da mesma maneira. A diferença é que um índice não clusterizado é um índice secundário criado em uma tabela rowstore, mas um índice columnstore clusterizado é o armazenamento primário da tabela inteira.  
  
O índice não clusterizado contém uma cópia de parte ou de todas as linhas e colunas na tabela subjacente. O índice é definido como uma ou mais colunas da tabela e tem uma condição opcional que filtra as linhas.  
  
Um índice não clusterizado columnstore permite análises operacionais em tempo real nas quais a carga de trabalho OLTP usa o índice clusterizado subjacente, enquanto as análises são executadas simultaneamente no índice columnstore. Para obter mais informações, veja [Introdução ao columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
#### <a name="batch-mode-execution"></a>Execução em modo de lote
A execução em modo de lote é um método de processamento de consulta usado para processar várias linhas simultaneamente. A execução em modo de lote é estreitamente integrada ao formato de armazenamento columnstore e otimizada com base nele. A execução do modo em lote às vezes é conhecida como execução *baseada em vetor* ou *vetorizada*. Consultas em índices columnstore usam a execução em modo de lote, o que melhora o desempenho de consulta normalmente em duas a quatro vezes. Para saber mais, confira o [Guia da arquitetura de processamento de consultas](../query-processing-architecture-guide.md#execution-modes). 
  
##  <a name="benefits"></a> Por que devo usar um índice columnstore?  
Um índice columnstore pode fornecer um nível muito alto de compactação de dados, geralmente de 10 vezes, para reduzir consideravelmente os custos de armazenamento em data warehouse. Para análises, um índice columnstore oferece um desempenho melhor de ordem de magnitude do que um índice de árvore B. Os índice columnstore são o formato de armazenamento de dados preferencial para data warehouse e cargas de trabalho de análise. A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode usar índices columnstore para análises em tempo real da sua carga de trabalho operacional.  
  
Motivos pelos quais índices columnstore são tão rápidos:  
  
-   Colunas armazenam valores do mesmo domínio e normalmente têm valores semelhantes, o que resulta em altas taxas de compactação. Os gargalos de E/S em seu sistema são minimizados ou eliminados, e o volume de memória é reduzido consideravelmente.  
  
-   As altas taxas de compactação melhoram o desempenho da consulta usando um menor volume na memória. Por sua vez, o desempenho da consulta pode ser melhorado porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode realizar mais operações de consulta e dados na memória.  
  
-   A execução em lote melhora o desempenho de consulta, normalmente em duas a quatro vezes, processando várias linhas simultaneamente.  
  
-   Muitas vezes, as consultas selecionam apenas algumas colunas de uma tabela, o que reduz a E/S total da mídia física.  
  
## <a name="when-should-i-use-a-columnstore-index"></a>Quando devo usar um índice columnstore?  
Casos de uso recomendados:  
  
-   Use um índice columnstore clusterizado para armazenar tabelas de fatos e tabelas de dimensões grandes para cargas de trabalho de data warehouse. Esse método melhora o desempenho de consulta e a compactação de dados em até 10 vezes. Para saber mais, consulte [Índices columnstore – data warehouse](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md).  
  
-   Use um índice columnstore não clusterizado para executar análises em tempo real em uma carga de trabalho OLTP. Para obter mais informações, veja [Introdução ao columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
### <a name="how-do-i-choose-between-a-rowstore-index-and-a-columnstore-index"></a>Como escolher entre um índice rowstore e um índice columnstore?  
Índices rowstore têm melhor desempenho em consultas nos dados, ao procurar um valor específico ou para consultas em um pequeno intervalo de valores. Use índices rowstore com cargas de trabalho transacionais, pois eles tendem a exigir principalmente buscas de tabela em vez de verificações de tabela.  
  
Os índices columnstore oferecem altos ganhos de desempenho para consultas analíticas que examinam grandes quantidades de dados, especialmente em tabelas grandes. Use índices columnstore em cargas de trabalho de data warehouse e análise, especialmente em tabelas de fatos, pois eles tendem a exigir verificações de tabela completas em vez de buscas de tabela.  
  
### <a name="can-i-combine-rowstore-and-columnstore-on-the-same-table"></a>Posso combinar rowstore e columnstore na mesma tabela?  
Sim. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar um índice columnstore não clusterizado atualizável em uma tabela rowstore. O índice columnstore armazena uma cópia das colunas selecionadas, então você precisa de espaço adicional para esses dados, mas os dados selecionados serão 10 vezes compactados, em média. Você pode executar análises no índice columnstore e transações no índice rowstore ao mesmo tempo. O columnstore é atualizado quando os dados são alterados na tabela rowstore, assim, ambos os índices trabalham com os mesmos dados.  
  
A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode ter um ou mais índices rowstore não clusterizado em um índice columnstore de índice, e executar pesquisas de tabela eficientes no columnstore subjacente. Outras opções também são disponibilizadas. Por exemplo, você pode impor uma restrição de chave primária usando uma restrição UNIQUE na tabela rowstore. Como um valor não exclusivo não pode ser inserido na tabela rowstore, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá inserir o valor no columnstore.  
  
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
  
## <a name="related-tasks"></a>Tarefas relacionadas  
Todas as tabelas relacionais usam rowstore como formato de dados subjacente, a menos que você as especifique como um índice columnstore clusterizado. `CREATE TABLE` cria uma tabela rowstore, a menos que a opção `WITH CLUSTERED COLUMNSTORE INDEX` seja especificada.  
  
Ao criar uma tabela com a instrução `CREATE TABLE`, você pode criar a tabela como um columnstore especificando a opção `WITH CLUSTERED COLUMNSTORE INDEX`. Caso já tenha uma tabela rowstore e deseje convertê-la em um columnstore, use a instrução `CREATE COLUMNSTORE INDEX`.  
  
|Tarefa|Tópicos de referência|Observações|  
|----------|----------------------|-----------|  
|Crie uma tabela como columnstore.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar a tabela como um índice columnstore clusterizado. Não é preciso criar primeiro uma tabela rowstore e convertê-la em columnstore.|  
|Crie uma tabela de memória com um índice columnstore.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar uma tabela com otimização na memória com um índice columnstore. O índice columnstore também pode ser adicionado após a criação da tabela, usando a sintaxe `ALTER TABLE ADD INDEX`.|  
|Converta uma tabela rowstore em columnstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Converta uma pilha ou árvore binária existente em columnstore. Exemplos mostram como lidar com os índices existentes e o nome do índice ao realizar essa conversão.|  
|Converta uma tabela columnstore em rowstore.|[CRIAR O ÍNDICE CLUSTERIZADO &#40;Transact-SQL&#41; ](../../t-sql/statements/create-columnstore-index-transact-sql.md#d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index) ou [Converter uma tabela columnstore novamente em um heap rowstore](../../t-sql/statements/create-columnstore-index-transact-sql.md#e-convert-a-columnstore-table-back-to-a-rowstore-heap) |Geralmente, essa conversão não é necessária, mas pode haver ocasiões em que você precisa realizá-la. Exemplos mostram como converter um columnstore em uma pilha ou um índice clusterizado.|  
|Crie um índice columnstore em uma tabela rowstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Uma tabela rowstore pode ter um índice columnstore. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o índice columnstore pode ter uma condição filtrada. Exemplos mostram a sintaxe básica.|  
|Crie índices de alto desempenho para análises operacionais.|[Introdução ao columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|Descreve como criar índices de árvore B e columnstore complementares para que consultas OLTP usem índices de árvore B e consultas de análise usem índices columnstore.|  
|Crie índices columnstore de alto desempenho para data warehouse.|[Índices columnstore para data warehouse](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Descreve como usar índices de árvore B em tabelas columnstore para criar consultas de data warehouse de alto desempenho.|  
|Use um índice de árvore B para impor uma restrição de chave primária em um índice columnstore.|[Índices columnstore para data warehouse](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Mostra como combinar índices columnstore e de árvore B para impor restrições de chave primária no índice columnstore.|  
|Remover um índice columnstore.|[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)|A remoção de um índice columnstore usa a sintaxe `DROP INDEX` padrão usada pelos índices de árvore B. A remoção de um índice columnstore clusterizado converte a tabela columnstore em uma pilha.|  
|Excluir uma linha de um índice columnstore.|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Use [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) para excluir uma linha.<br /><br /> **linha columnstore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca a linha como excluída logicamente, mas não recupera o armazenamento físico da linha até que o índice seja recriado.<br /><br /> **linha deltastore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui a linha lógica e fisicamente.|  
|Atualizar uma linha no índice columnstore.|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|Use [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) para atualizar uma linha.<br /><br /> **linha columnstore**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca a linha como excluída logicamente e insere a linha atualizada no deltastore.<br /><br /> **linha deltastore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualiza a linha no deltastore.|  
|Carregar dados em um índice columnstore.|[Carregamento de dados dos índices columnstore](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)||  
|Força todas as linhas no deltastore a ir para o columnstore.|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) ... `REBUILD`<br /><br /> [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)|`ALTER INDEX` com a opção `REBUILD` força todas as linhas a ir para o columnstore.|  
|Desfragmentar um índice columnstore.|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)|`ALTER INDEX ... REORGANIZE` desfragmenta os índices columnstore online.|  
|Mescle tabelas com índices columnstore.|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)||  
  
## <a name="see-also"></a>Confira também  
 [Carregamento de dados dos índices columnstore](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Resumo de recursos com versão dos índices columnstore](~/relational-databases/indexes/columnstore-indexes-what-s-new.md)   
 [Desempenho de consultas de índices columnstore](~/relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Introdução ao columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Índices columnstore para data warehouse](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Desfragmentação de índices columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)   
 [Guia de criação de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md)   
 [Arquitetura de índices columnstore](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)   
  
  
