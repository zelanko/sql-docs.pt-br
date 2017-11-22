---
title: "Índices columnstore – arquitetura | Microsoft Docs"
ms.custom: 
ms.date: 01/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 96b8e884-8244-425f-b856-72a8ff6895a6
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 64914f8620c848cf7505253c3b517486a53ad14e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="columnstore-indexes---architecture"></a>Índices columnstore – arquitetura
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Saiba como um índice columnstore é arquitetado. Com estas noções básicas ficará mais fácil entender outros artigos sobre columnstore que explicam como usá-los com eficiência.

## <a name="data-storage-uses-columnstore-and-rowstore-compression"></a>O armazenamento de dados usa compactação de columnstore e rowstore
Em discussões sobre índices columnstore, usamos os termos *rowstore* e *columnstore* para enfatizar o formato do armazenamento de dados.  Os índices columnstore usam os dois tipos de armazenamento.

 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")

- Um **columnstore** são dados organizados logicamente como uma tabela com linhas e colunas e armazenados fisicamente em um formato de dados com reconhecimento de colunas.
  
Um índice columnstore armazena fisicamente a maioria dos dados no formato columnstore. No formato columnstore, os dados são compactados e descompactados como colunas. Não é necessário descompactar outros valores em cada linha que não sejam solicitados pela consulta. Isso acelera a verificação de uma coluna inteira de uma tabela grande. 

- Um **rowstore** são dados organizados logicamente como uma tabela com linhas e colunas e armazenados fisicamente em um formato de dados com reconhecimento de linha. Essa tem sido a maneira tradicional de armazenar dados de tabelas relacionais, como um índice "de árvore B" de heap ou clusterizado.

Um índice columnstore também armazena fisicamente algumas linhas em um formato de rowstore, chamado deltastore. O deltastore, também chamado de rowgroups delta, é um espaço reservado para linhas que são muito poucas para se qualificarem para compactação no columnstore. Cada rowgroup delta é implementado como um índice de árvore B clusterizado. 

- Um **deltastore** é um local de espera para linhas que são muito poucas para serem compactadas no columnstore. O deltastore é um rowstore. 
  
## <a name="operations-are-performed-on-rowgroups-and-column-segments"></a>Operações são executadas em rowgroups e em segmentos de colunas

O índice columnstore agrupa linhas em unidades gerenciáveis. Cada uma dessas unidades é chamada de rowgroup. Para melhor desempenho, o número de linhas em um rowgroup é grande o suficiente para melhorar as taxas de compactação e pequeno o suficiente para beneficiar-se de operações na memória.

* Um **rowgroup** é um grupo de linhas em que o índice columnstore executa operações de gerenciamento e compactação. 

Por exemplo, o índice columnstore executa estas operações em rowgroups:

* Compacta rowgroups no columnstore. A compactação é executada em cada segmento de coluna dentro de um rowgroup.
* Mescla rowgroups durante uma operação ALTER INDEX REORGANIZE.
* Cria novos rowgroups durante uma operação ALTER INDEX REBUILD.
* Relata a integridade e a fragmentação do rowgroup nas DMVs (exibições de gerenciamento dinâmico).

O deltastore é composto de um ou mais rowgroups chamados rowgroups delta. Cada rowgroup delta é um índice de árvore B clusterizado que armazena linhas quando elas são muito poucas para serem compactadas no columnstore.  

* Um **rowgroup delta** é um índice de árvore B clusterizado que armazena pequenas cargas e inserções em massa até que o rowgroup contenha 1.048.576 linhas ou até que o índice seja recriado.  Quando um rowgroup delta contém 1.048.576 linhas, ele é marcado como fechado e espera por um processo chamado motor de tupla para compactá-lo no columnstore. 


Cada coluna tem alguns de seus valores em cada rowgroup. Esses valores são chamados de segmentos de coluna. Quando o índice columnstore compacta um rowgroup, ele compacta cada segmento de coluna separadamente. Para descompactar uma coluna inteira, o índice columnstore só precisa descompactar um segmento de coluna de cada rowgroup.

* Um **segmento de coluna** é a parte de valores de coluna em um rowgroup. Cada rowgroup contém um segmento de coluna para cada coluna na tabela. Cada coluna tem um segmento de coluna em cada rowgroup.| 
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
 
## <a name="small-loads-and-inserts-go-to-the-deltastore"></a>Cargas e inserções pequenas vão para o deltastore
Um índice columnstore melhora a compactação e o desempenho do columnstore por compactar pelo menos 102.400 linhas por vez no índice columnstore. Para compactar linhas em massa, o índice columnstore acumula pequenas cargas e insere no deltastore. As operações de deltastore são tratadas em segundo plano. Para retornar os resultados corretos da consulta, o índice columnstore clusterizado combina os resultados da consulta de columnstore e deltastore. 

As linhas vão para o deltastore quando:
* São inseridas com a instrução INSERT INTO VALUES.
* Estão no final de uma carga em massa e em número menor de 102.400.
* São atualizadas. Cada atualização é implementada como uma exclusão e uma inserção.

O deltastore também armazena uma lista de IDs de linhas excluídas que foram marcadas como excluídas, mas ainda não foram excluídas fisicamente do columnstore. 

## <a name="when-delta-rowgroups-are-full-they-get-compressed-into-the-columnstore"></a>Quando os rowgroups delta estão cheios, eles são compactados para o columnstore

Os índices columnstore clusterizados coletam até 1.048.576 linhas em cada rowgroup delta antes de compactar o rowgroup no columnstore. Isso melhora a compactação do índice columnstore. Quando um rowgroup delta contém 1.048.576 linhas, o índice columnstore marca o rowgroup como fechado. Um processo em segundo plano, chamado *motor de tupla*, localiza cada rowgroup fechado e compacta-o no columnstore. 

Você pode forçar rowgroups delta para o columnstore usando [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) para reccompilar ou reorganizar o índice.  Observe que, se houver pressão de memória durante a compactação, o índice columnstore poderá reduzir o número de linhas no rowgroup compactado.

## <a name="each-table-partition-has-its-own-rowgroups-and-delta-rowgroups"></a>Cada partição de tabela tem seus próprios rowgroups e rowgroups delta

O conceito de particionamento é o mesmo em um índice clusterizado, um heap e um índice columnstore. Particionar uma tabela divide a tabela em grupos menores de linhas de acordo com um intervalo de valores de coluna. Geralmente, ele é usado para gerenciar os dados. Por exemplo, você pode criar uma partição para cada ano de dados e usar a alternância de partição para arquivar dados em um armazenamento mais barato. A alternância de partição funciona em índices columnstore e facilita a movimentação de uma partição de dados para outro local.

Os rowgroups sempre são definidos dentro de uma partição de tabela. Quando um índice columnstore é particionado, cada partição tem seus próprios rowgroups compactados e rowgroups delta.

### <a name="each-partition-can-have-multiple-delta-rowgroups"></a>Cada partição pode ter vários rowgroups delta
Cada partição pode ter mais de um rowgroup delta. Quando o índice columnstore precisar adicionar dados a um rowgroup delta e o rowgroup delta estiver bloqueado, o índice columnstore tentará obter um bloqueio em um rowgroup delta diferente. Se não houver nenhum rowgroup delta disponível, o índice columnstore criará um novo rowgroup delta.  Por exemplo, uma tabela com 10 partições poderia facilmente ter 20 ou mais rowgroups delta. 

  
## <a name="you-can-combine-columnstore-and-rowstore-indexes-on-the-same-table"></a>Você pode combinar índices columnstore e rowstore na mesma tabela
Um índice não clusterizado contém uma cópia de parte ou de todas as linhas e colunas na tabela subjacente. O índice é definido como uma ou mais colunas da tabela e tem uma condição opcional que filtra as linhas. 

Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar um índice columnstore não clusterizado atualizável em uma tabela rowstore. O índice columnstore armazena uma cópia dos dados, portanto, você precisa de armazenamento extra. No entanto, os dados no índice columnstore serão compactados em um tamanho menor do que a tabela rowstore precisa.  Com isso, você pode executar análises no índice columnstore e transações no índice rowstore ao mesmo tempo. O repositório de colunas é atualizado quando dados são alterados na tabela rowstore, assim, ambos os índices trabalham com os mesmos dados.  
  
 Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode ter um ou mais índices rowstore não clusterizados em um índice columnstore. Fazendo isso, você pode executar buscas de tabela eficientes no columnstore subjacente. Outras opções também são disponibilizadas. Por exemplo, você pode impor uma restrição de chave primária usando uma restrição UNIQUE na tabela rowstore. Como um valor não exclusivo não poderá ser inserido na tabela rowstore, o SQL Server não pode inserir o valor no columnstore.  
 

## <a name="metadata"></a>Metadados  
Use essas exibições de metadados para ver os atributos de índices columnstore. Mais informações arquitetônicas são inseridas em algumas dessas exibições.

Observe que todas as colunas em um índice columnstore são armazenadas nos metadados como colunas incluídas. O índice columnstore não tem colunas de chave.  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
  
-   [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)  
  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)  
  
-   [sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
|  


## <a name="next-steps"></a>Próximas etapas
 Para obter diretrizes sobre como criar índices columnstore, consulte [Columnstore indexes – design guidance](../../relational-databases/indexes/columnstore-indexes-design-guidance.md) (Índices columnstore – diretrizes de design)
