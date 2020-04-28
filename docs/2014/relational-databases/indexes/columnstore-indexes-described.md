---
title: Índices Columnstore descritos | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6220d6650d2be81cad3f38862ba74213219a28a0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175911"
---
# <a name="columnstore-indexes-described"></a>Columnstore Indexes Described
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *índice columnstore na memória* armazena e gerencia dados usando o armazenamento de dados baseado em coluna e o processamento de consulta baseado em coluna. Os índices columnstore funcionam bem para as cargas de trabalho de data warehouse que executam principalmente carregamentos em massa e consultas somente leitura. Use o índice columnstore para obter um ganho de **desempenho de consulta até 10 vezes maior** sobre o armazenamento tradicional orientado por linha e de **compactação de dados até 7 vezes maior** sobre o tamanho dos dados não compactados.

> [!NOTE]
>  Exibimos o índice columnstore clusterizado como o padrão para armazenar grandes tabelas de fatos de data warehouse e esperamos que ele seja usado na maioria dos cenários de data warehouse. Uma vez que o índice columnstore clusterizado é atualizável, a carga de trabalho pode executar um grande número de operações de inserção, atualização e exclusão.

## <a name="contents"></a>Conteúdo

-   [Noções básicas](#basics)

-   [Carregando dados](#dataload)

-   [Dicas de desempenho](#performance)

-   [Tarefas e tópicos relacionados](#related)

##  <a name="basics"></a><a name="basics"></a>Algumas
 Um *índice columnstore* é uma tecnologia para armazenar, recuperar e gerenciar dados usando um formato de dados de coluna, chamado columnstore. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte a índices columnstore clusterizados e não clusterizados. Ambos usam a mesma tecnologia de columnstore na memória, mas possuem diferenças na finalidade e nos recursos aos quais oferecem suporte.

###  <a name="benefits"></a><a name="benefits"></a>Benefícios
 Os índices columnstore funcionam bem na maioria das consultas somente leitura que executam a análise em grandes conjuntos de dados. Geralmente, essas são consultas sobre cargas de trabalho de data warehousing. Os índices columnstore permitem ganhos de desempenho alto para consultas que usam digitalizações completas de tabela e não são apropriados para consultas que buscam nos dados, procurando um valor específico.

 Benefícios do índice columnstore:

-   As colunas muitas vezes têm dados semelhantes, o que resulta em altas taxas de compactação.

-   As altas taxas de compactação melhoram o desempenho da consulta usando um menor volume na memória. Por sua vez, o desempenho da consulta pode ser melhorado porque o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode realizar mais operações de consulta e dados na memória.

-   Um novo mecanismo de execução de consulta chamado execução do modo em lotes foi adicionado ao SQL Server, o que reduz bastante o uso da CPU. A execução do modo em lotes é integrada ao formato de armazenamento columnstore e otimizado com base nele. A execução do modo em lote às vezes é conhecida como execução baseada em vetor ou vetorizado.

-   Muitas vezes, as consultas selecionam apenas algumas colunas de uma tabela, o que reduz a E/S total da mídia física.

### <a name="columnstore-versions"></a>Versões de columnstore
 O SQL Server 2012, o SQL Server 2012 Parallel Data Warehouse e o SQL Server 2014 usam índices columnstore para acelerar consultas comuns de data warehouse. O SQL Server 2012 apresentou dois novos recursos: um índice columnstore não clusterizado e um recurso de execução de consulta baseada em vetor que processa dados em unidades chamadas "lotes". O SQL Server 2014 tem os recursos do SQL Server 2012 mais os índices columnstore clusterizados atualizáveis.

### <a name="key-characteristics"></a>Principais características

||
|-|
|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].|

 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um índice columnstore clusterizado:

-   Está disponível nas edições Enterprise, Developer e Evaluation.

-   É atualizável.

-   É o método de armazenamento primário para toda a tabela.

-   Não tem colunas de chave. Todas as colunas são colunas incluídas.

-   É o único índice na tabela. Não pode ser combinado com nenhum outro índice.

-   Pode ser configurado para usar a columnstore ou compressão de arquivamento columnstore.

-   Não armazena fisicamente colunas em uma ordem classificada. Em vez disso, ele armazena dados para aprimorar a compactação e o desempenho.

||
|-|
|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].|

 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um índice columnstore não clusterizado:

-   Pode indexar um subconjunto das colunas no índice clusterizado ou heap. Por exemplo, pode indexar as colunas frequentemente usadas.

-   Exige armazenamento extra para armazenar uma cópia das colunas no índice.

-   É atualizado com a recriação do índice ou a alternância entre e saída de partições. Ele não é atualizável usando as operações DML, como INSERT, Update e Delete.

-   Pode ser combinado com outros índices na tabela.

-   Pode ser configurado para usar a columnstore ou compressão de arquivamento columnstore.

-   Não armazena fisicamente colunas em uma ordem classificada. Em vez disso, ele armazena dados para aprimorar a compactação e o desempenho. A pré-classificação de dados antes da criação do índice columnstore não é necessária, mas pode melhorar a compactação columnstore.

###  <a name="key-concepts-and-terms"></a><a name="Concepts"></a>Principais conceitos e termos
 Os termos e conceitos principais a seguir estão associados aos índices columnstore.

 índice columnstore um *índice columnstore* é uma tecnologia para armazenar, recuperar e gerenciar dados usando um formato de dados de coluna, chamado columnstore. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte a índices columnstore clusterizados e não clusterizados. Ambos usam a mesma tecnologia de columnstore na memória, mas possuem diferenças na finalidade e nos recursos aos quais oferecem suporte.

 columnstore um *columnstore* são dados organizados logicamente como uma tabela com linhas e colunas e fisicamente armazenados em um formato de dados de coluna.

 o rowgroup é um *armazenamento* de dados que é organizado logicamente como uma tabela com linhas e colunas e, em seguida, armazenado fisicamente em um formato de dados de linha. Esse tem sido o modo tradicional de armazenar dados da tabela relacional.

 os grupos de linhas e de colunas para altas taxas de alto desempenho e alta compactação, o índice columnstore fatiam a tabela em grupos de linha, chamados de grupo de linhas e, em seguida, compacta cada grupo de linhas de forma inteligente. O número de linhas no grupo de linhas deve ser grande o suficiente para melhorar as taxas de compactação e pequeno o suficiente para se beneficiar com as operações na memória.

 grupo *de linhas um rowgroup é um* grupo de linhas que são compactadas no formato columnstore ao mesmo tempo.

 segmento de coluna um *segmento de coluna* é uma coluna de dados de dentro do rowgroup.

-   Um grupo de linhas normalmente contém o número máximo de linhas por grupo de linhas que é 1.048.576 linhas.

-   Cada rowgroup contém um segmento de coluna para cada coluna na tabela.

-   Cada segmento de coluna é compactado junto e armazenado em meio físico.

 ![Segmento de coluna](../../database-engine/media/sql-server-pdw-columnstore-columnsegment.gif "segmento de coluna")

 índice columnstore não clusterizado um *índice columnstore não clusterizado* é um índice somente leitura criado em um índice clusterizado ou tabela de heap existente. Contém uma cópia de um subconjunto de colunas, até e incluindo todas as colunas na tabela. A tabela é somente leitura enquanto contém um índice columnstore não clusterizado.

 Um índice columnstore não clusterizado fornece uma maneira de ter um índice columnstore para execução de consultas de análise e, ao mesmo tempo, executar operações somente leitura na tabela original.

 ![Índice columnstore não clusterizado](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage-nonclustered.gif "índice columnstore não clusterizado")

 índice columnstore clusterizado um *índice columnstore clusterizado* é o armazenamento físico para a tabela inteira e é o único índice para a tabela. O índice clusterizado é atualizável. Você pode executar operações de inserção, exclusão e atualização no índice e pode carregar dados em massa no índice.

 ![Índice Columnstore clusterizado](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage.gif "Índice columnstore clusterizado")

 Para reduzir a fragmentação dos segmentos de coluna e melhorar o desempenho, o índice columnstore pode armazenar alguns dados temporariamente em uma tabela rowstore, chamada deltastore, mais uma árvore B de IDs para as linhas excluídas. As operações de deltastore são tratadas em segundo plano. Para retornar os resultados corretos da consulta, o índice columnstore clusterizado combina os resultados da consulta de columnstore e deltastore.

 deltastore usado somente com índices columnstore clusterizados, um *deltastore* é uma tabela do RowNumber que armazena linhas até que o número de linhas seja grande o suficiente para ser movido para o columnstore. Um deltastore é usado com índices columnstore clusterizados para melhorar o desempenho do carregamento e de outras operações DML.

 Durante o carregamento em massa grande, a maioria das linhas vai diretamente para o columnstore sem passar pelo deltastore. No fim do carregamento em massa, o número de linhas pode ser muito pouco para atender ao tamanho mínimo de um rowgroup, que é de 102.400 linhas. Quando isso ocorre, as linhas finais vão para o deltastore, e não para o columnstore. Para carregamento em massa pequeno, menos de 102.400 linhas, todas as linhas vão diretamente para o deltastore.

 Quando o deltastore atinge o número máximo de linhas, ele é fechado. Um processo de movimentação de tupla verifica os grupos de linhas fechados. Quando encontra o grupo de linhas fechado, compacta-o e armazena-o no columnstore.

##  <a name="loading-data"></a><a name="dataload"></a>Carregando dados

###  <a name="loading-data-into-a-nonclustered-columnstore-index"></a><a name="dataload_nci"></a>Carregando dados em um índice Columnstore não clusterizado
 Para carregar dados em um índice columnstore não clusterizado, primeiro carregue dados em uma tabela de armazenamento tradicional armazenada como um índice de heap ou cluster e, em seguida, crie o índice columnstore não clusterizado com [Create COLUMNSTORE index &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-columnstore-index-transact-sql).

 ![Carregando dados em um índice columnstore](../../database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "Carregando dados em um índice columnstore")

 Uma tabela com um índice columnstore não clusterizado é somente leitura até que o índice seja removido ou desabilitado. Para atualizar a tabela e o índice columnstore não clusterizado, você pode alternar as partições para dentro e para fora. Você também pode desabilitar o índice, atualizar a tabela e, em seguida, recompilar o índice.

 Para obter mais informações, consulte [Using Nonclustered Columnstore Indexes](indexes.md)

###  <a name="loading-data-into-a-clustered-columnstore-index"></a><a name="dataload_cci"></a>Carregando dados em um índice Columnstore clusterizado
 ![Carregamento em um índice columnstore clusterizado](../../database-engine/media/sql-server-pdw-columnstore-loadprocess.gif "Carregamento em um índice columnstore clusterizado")

 Como sugere o diagrama, para carregar dados em um índice columnstore clusterizado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:

1.  Insere rowgroups de tamanho máximo diretamente no columnstore. À medida que os dados são carregados, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] atribui as linhas de dados por ordem de chegada em um rowgroup aberto.

2.  Para cada rowgroup, depois que ele atinge o tamanho máximo, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:

    1.  Marca o rowgroup como CLOSED.

    2.  Ignora o deltastore.

    3.  Compacta cada segmento de coluna com o rowgroup com a compactação columnstore.

    4.  Armazena fisicamente cada segmento de coluna compactado no columnstore.

3.  Insere as linhas restantes no columnstore ou deltastore, como se segue:

    1.  Se o número de linhas atender ao requisito de linhas mínimas por rowgroup, as linhas serão adicionadas ao columnstore.

    2.  Se o número de linhas for menor que o mínimo de linhas por rowgroup, as linhas serão adicionadas ao deltastore.

 Para obter mais informações sobre tarefas e processos de deltastore, consulte [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md)

##  <a name="performance-tips"></a><a name="performance"></a>Dicas de desempenho

### <a name="plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>Planejar memória suficiente para criar índices columnstore em paralelo
 Criar um índice columnstore é, por padrão, uma operação paralela, a menos que a memória seja restrita. Criar o índice em paralelo exige mais memória do que criar o índice em série. Quando há bastante memória, a criação de um índice columnstore assume a ordem de 1,5 vezes mais longa do que a criação de uma árvore B nas mesmas colunas.

 A memória necessária para criar um índice columnstore depende do número de colunas, do número de colunas de cadeia de caracteres, do grau de paralelismo (DOP) e as características dos dados. Por exemplo, se sua tabela tiver menos de um milhão de linhas, o SQL Server usará apenas um thread para criar o índice columnstore.

 Se a sua tabela tiver mais de um milhão de linhas, mas o SQL Server não puder obter uma quantidade de memória suficiente para criar o índice usando MAXDOP, o SQL Server diminuirá automaticamente MAXDOP conforme o necessário de acordo com a quantidade de memória disponível.  Em alguns casos, o DOP deve ser diminuído para um para criar o índice na memória restrita.

##  <a name="related-tasks-and-topics"></a><a name="related"></a>Tópicos e tarefas relacionadas

### <a name="nonclustered-columnstore-indexes"></a>Índices columnstore não clusterizados
 Para tarefas comuns, consulte [Using Nonclustered Columnstore Indexes](../../database-engine/using-nonclustered-columnstore-indexes.md).

-   [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [ALTER INDEX &#40;&#41;Transact-SQL](/sql/t-sql/statements/alter-index-transact-sql) com recompilação.

-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)

### <a name="clustered-columnstore-indexes"></a>Índices columnstore clusterizados
 Para tarefas comuns, consulte [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md).

-   [CRIAR índice COLUMNSTORE CLUSTERIZAdo &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [ALTER INDEX &#40;&#41;Transact-SQL](/sql/t-sql/statements/alter-index-transact-sql) com recompilação ou reorganização.

-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)

-   [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)

-   [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)

-   [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)

### <a name="metadata"></a>Metadados
 Todas as colunas em um índice columnstore são armazenadas nos metadados como colunas incluídas. O índice columnstore não tem colunas de chave.

-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)

-   [sys.index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)

-   [sys.partitions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql)

-   [sys.column_store_segments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-segments-transact-sql)

-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql)

-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)


