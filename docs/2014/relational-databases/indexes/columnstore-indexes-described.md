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
ms.openlocfilehash: 87d19bc837219b5573dd237310b11dab9f146406
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "68811042"
---
# <a name="columnstore-indexes-described"></a>Índices Columnstore descritos
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *índice columnstore na memória* armazena e gerencia dados usando o armazenamento de dados baseado em coluna e o processamento de consulta baseado em coluna. Os índices Columnstore funcionam bem para cargas de trabalho de data warehouse que executam principalmente cargas em massa e consultas somente leitura. Use o índice columnstore para alcançar ganhos de **desempenho de consulta de até 10 vezes** no armazenamento tradicional orientado por linha e até a **compactação de dados de 7x** em relação ao tamanho de dados descompactado.  
  
> [!NOTE]  
>  Exibimos o índice columnstore clusterizado como o padrão para armazenar grandes tabelas de fatos de data warehouse e esperamos que ele seja usado na maioria dos cenários de data warehouse. Como o índice columnstore clusterizado é atualizável, sua carga de trabalho pode executar um grande número de operações de inserção, atualização e exclusão.  
  
## <a name="contents"></a>Índice  
  
-   [Algumas](#basics)  
  
-   [Carregando dados](#dataload)  
  
-   [Dicas de desempenho](#performance)  
  
-   [Tópicos e tarefas relacionadas](#related)  
  
##  <a name="basics"></a>Algumas  
 Um *índice columnstore* é uma tecnologia para armazenar, recuperar e gerenciar dados usando um formato de dados de coluna, chamado columnstore. o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a índices columnstore clusterizados e não clusterizados. Ambos usam a mesma tecnologia columnstore na memória, mas têm diferenças na finalidade e nos recursos aos quais eles dão suporte.  
  
###  <a name="benefits"></a>Benefícios  
 Os índices Columnstore funcionam bem para consultas somente leitura que executam análise em grandes conjuntos de dados. Geralmente, essas são consultas sobre cargas de trabalho de data warehousing. Os índices Columnstore oferecem ganhos de alto desempenho para consultas que usam verificações de tabela completas e não são adequados para consultas que buscam os dados, procurando um valor específico.  
  
 Benefícios do índice columnstore:  
  
-   As colunas muitas vezes têm dados semelhantes, o que resulta em altas taxas de compactação.  
  
-   Altas taxas de compactação melhoram o desempenho da consulta usando um espaço na memória menor. Por sua vez, o desempenho da consulta pode melhorar porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode executar mais operações de consulta e dados na memória.  
  
-   Um novo mecanismo de execução de consulta chamado execução em modo de lote foi adicionado ao SQL Server que reduz o uso da CPU por um grande volume. A execução em modo de lote é totalmente integrada ao formato de armazenamento columnstore e otimizado. Às vezes, a execução em modo de lote é conhecida como execução vetorial ou vetorial.  
  
-   As consultas geralmente selecionam apenas algumas colunas de uma tabela, o que reduz a e/s total da mídia física.  
  
### <a name="columnstore-versions"></a>Versões de columnstore  
 O SQL Server 2012, o SQL Server 2012 Parallel Data Warehouse e o SQL Server 2014 usam índices columnstore para acelerar consultas comuns de data warehouse. O SQL Server 2012 introduziu dois novos recursos: um índice columnstore não clusterizado e um recurso de execução de consulta baseado em vetor que processa dados em unidades chamadas "lotes". O SQL Server 2014 tem os recursos do SQL Server 2012 mais os índices columnstore clusterizados atualizáveis.  
  
### <a name="key-characteristics"></a>Principais características  
  
||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].|  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um índice columnstore clusterizado:  
  
-   Está disponível nas edições Enterprise, Developer e Evaluation.  
  
-   É atualizável.  
  
-   É o método de armazenamento primário para a tabela inteira.  
  
-   Não tem colunas de chave. Todas as colunas são colunas incluídas.  
  
-   É o único índice na tabela. Ele não pode ser combinado com nenhum outro índice.  
  
-   Pode ser configurado para usar a compactação columnstore ou de arquivamento columnstore.  
  
-   Não armazena fisicamente colunas em uma ordem classificada. Em vez disso, ele armazena dados para melhorar a compactação e o desempenho.  
  
||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].|  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um índice columnstore não clusterizado:  
  
-   Pode indexar um subconjunto de colunas no índice ou heap clusterizado. Por exemplo, ele pode indexar as colunas usadas com frequência.  
  
-   Exige armazenamento extra para armazenar uma cópia das colunas no índice.  
  
-   É atualizado com a recriação do índice ou a alternância entre e saída de partições. Ele não é atualizável usando as operações DML, como INSERT, Update e Delete.  
  
-   Pode ser combinado com outros índices na tabela.  
  
-   Pode ser configurado para usar a compactação columnstore ou de arquivamento columnstore.  
  
-   Não armazena fisicamente colunas em uma ordem classificada. Em vez disso, ele armazena dados para melhorar a compactação e o desempenho. Não é necessário classificar previamente os dados antes de criar o índice columnstore, mas pode melhorar a compactação columnstore.  
  
###  <a name="Concepts"></a>Principais conceitos e termos  
 Os termos e conceitos principais a seguir estão associados a índices columnstore.  
  
 índice columnstore  
 Um *índice columnstore* é uma tecnologia para armazenar, recuperar e gerenciar dados usando um formato de dados de coluna, chamado columnstore. o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a índices columnstore clusterizados e não clusterizados. Ambos usam a mesma tecnologia columnstore na memória, mas têm diferenças na finalidade e nos recursos aos quais eles dão suporte.  
  
 columnstore  
 Um *columnstore* são dados que são logicamente organizados como uma tabela com linhas e colunas, e fisicamente armazenados em um formato de dados com sabedoria de coluna.  
  
 rowstore  
 Um *rowgroup* são dados organizados logicamente como uma tabela com linhas e colunas e, em seguida, armazenados fisicamente em um formato de dados de linha. Essa foi a maneira tradicional de armazenar dados de tabela relacional.  
  
 RowGroups e segmentos de coluna  
 Para altas taxas de desempenho e alta compactação, o índice columnstore fatia a tabela em grupos de linhas, chamados grupos de linhas, e, em seguida, compacta cada grupo de linhas de forma inteligente. O número de linhas no grupo de linhas deve ser grande o suficiente para melhorar as taxas de compactação e pequeno o suficiente para se beneficiar das operações na memória.  
  
 grupo de linhas  
 Um *rowgroup é um* grupo de linhas que são compactadas no formato columnstore ao mesmo tempo.  
  
 segmento de coluna  
 Um *segmento de coluna* é uma coluna de dados de dentro do rowgroup.  
  
-   Um grupo de linhas normalmente contém o número máximo de linhas por grupo de linhas que é 1.048.576 linhas.  
  
-   Cada rowgroup contém um segmento de coluna para cada coluna na tabela.  
  
-   Cada segmento de coluna é compactado em conjunto e armazenado em mídia física.  
  
 ![Segmento de coluna](../../database-engine/media/sql-server-pdw-columnstore-columnsegment.gif "segmento de coluna")  
  
 índice columnstore não clusterizado  
 Um *índice columnstore não clusterizado* é um índice somente leitura criado em um índice clusterizado ou tabela de heap existente. Contém uma cópia de um subconjunto de colunas, até e incluindo todas as colunas na tabela. A tabela é somente leitura enquanto contém um índice columnstore não clusterizado.  
  
 Um índice columnstore não clusterizado fornece uma maneira de ter um índice columnstore para executar consultas de análise e, ao mesmo tempo, executar operações somente leitura na tabela original.  
  
 ![Índice columnstore não clusterizado](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage-nonclustered.gif "índice columnstore não clusterizado")  
  
 índice columnstore clusterizado  
 Um *índice columnstore clusterizado* é o armazenamento físico para a tabela inteira e é o único índice para a tabela. O índice clusterizado é atualizável. Você pode executar operações de inserção, exclusão e atualização no índice e pode carregar dados em massa no índice.  
  
 ![Índice Columnstore clusterizado](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage.gif "Índice Columnstore clusterizado")  
  
 Para reduzir a fragmentação dos segmentos de coluna e melhorar o desempenho, o índice columnstore pode armazenar alguns dados temporariamente em uma tabela de repositório de linhas, chamada de deltastore, além de uma árvore B de IDs para filas excluídas. As operações deltastore são manipuladas em segundo plano. Para retornar os resultados de consulta corretos, o índice columnstore clusterizado combina os resultados da consulta do columnstore e do deltastore.  
  
 deltastore  
 Usado somente com índices columnstore clusterizados, um *deltastore* é uma tabela do RowNumber que armazena linhas até que o número de linhas seja grande o suficiente para ser movido para o columnstore. Um deltastore é usado com índices columnstore clusterizados para melhorar o desempenho do carregamento e de outras operações DML.  
  
 Durante um grande carregamento em massa, a maioria das linhas vai diretamente para o columnstore sem passar pelo deltastore. Algumas linhas no final do carregamento em massa podem ser muito poucas no número para atender ao tamanho mínimo de um rowgroup que é de 102.400 linhas. Quando isso acontece, as linhas finais vão para o deltastore em vez do columnstore. Para pequenas cargas em massa com menos de 102.400 linhas, todas as linhas vão diretamente para o deltastore.  
  
 Quando o deltastore atinge o número máximo de linhas, ele se torna fechado. Um processo de movimentação de tupla verifica os grupos de linhas fechados. Quando encontra o grupo de linhas fechado, compacta-o e armazena-o no columnstore.  
  
##  <a name="dataload"></a>Carregando dados  
  
###  <a name="dataload_nci"></a>Carregando dados em um índice Columnstore não clusterizado  
 Para carregar dados em um índice columnstore não clusterizado, primeiro carregue os dados em uma tabela de armazenamento tradicional armazenada como um índice de heap ou cluster e, em seguida, crie o índice columnstore não clusterizado com [Create &#40;columnstore&#41; index Transact-SQL](/sql/t-sql/statements/create-columnstore-index-transact-sql) .  
  
 ![Carregando dados em um índice columnstore](../../database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "Carregando dados em um índice columnstore")  
  
 Uma tabela com um índice columnstore não clusterizado é somente leitura até que o índice seja descartado ou desabilitado. Para atualizar a tabela e o índice columnstore não clusterizado, você pode alternar as partições para dentro e para fora. Você também pode desabilitar o índice, atualizar a tabela e, em seguida, recompilar o índice.  
  
 Para obter mais informações, consulte [usando índices Columnstore não clusterizados](indexes.md)  
  
###  <a name="dataload_cci"></a>Carregando dados em um índice Columnstore clusterizado  
 ![Carregando em um índice columnstore clusterizado](../../database-engine/media/sql-server-pdw-columnstore-loadprocess.gif "Carregando em um índice columnstore clusterizado")  
  
 Como sugere o diagrama, para carregar dados em um índice columnstore clusterizado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
1.  Insere grupos de colunas de tamanho máximo diretamente no columnstore. À medida que os dados são carregados, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] atribui as linhas de dados em uma primeira ordem de servi-la em um rowgroup aberto.  
  
2.  Para cada rowgroup, depois que ele atinge o tamanho máximo, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
    1.  Marca o rowgroup como fechado.  
  
    2.  Ignora o deltastore.  
  
    3.  Compacta cada segmento de coluna com o rowgroup com compactação columnstore.  
  
    4.  Armazena fisicamente cada segmento de coluna compactado no columnstore.  
  
3.  Insere as linhas restantes no columnstore ou deltastore da seguinte maneira:  
  
    1.  Se o número de linhas atender ao requisito mínimo de linhas por rowgroup, as linhas serão adicionadas ao columnstore.  
  
    2.  Se o número de linhas for menor que o mínimo de linhas por rowgroup, as linhas serão adicionadas ao deltastore.  
  
 Para obter mais informações sobre tarefas e processos do deltastore, consulte [usando índices Columnstore clusterizados](../../database-engine/using-clustered-columnstore-indexes.md)  
  
##  <a name="performance"></a>Dicas de desempenho  
  
### <a name="plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>Planejar memória suficiente para criar índices columnstore em paralelo  
 A criação de um índice columnstore é, por padrão, uma operação paralela, a menos que a memória seja restrita. Criar o índice em paralelo exige mais memória do que criar o índice em série. Quando há muita memória, a criação de um índice columnstore assume a ordem de 1,5 vezes desde a criação de uma árvore B nas mesmas colunas.  
  
 A memória necessária para criar um índice columnstore depende do número de colunas, do número de colunas de cadeia de caracteres, do DOP (grau de paralelismo) e das características dos dados. Por exemplo, se a tabela tiver menos de 1 milhão linhas, SQL Server usará apenas um thread para criar o índice columnstore.  
  
 Se a tabela tiver mais de 1 milhão linhas, mas SQL Server não puder obter uma concessão de memória suficiente grande para criar o índice usando MAXDOP, SQL Server diminuirá automaticamente o MAXDOP conforme necessário para se ajustar à concessão de memória disponível.  Em alguns casos, DOP deve ser diminuído para um a fim de criar o índice sob a memória restrita.  
  
##  <a name="related"></a>Tópicos e tarefas relacionadas  
  
### <a name="nonclustered-columnstore-indexes"></a>Índices Columnstore não clusterizados  
 Para tarefas comuns, consulte [usando índices Columnstore não clusterizados](../../database-engine/using-nonclustered-columnstore-indexes.md).  
  
-   [CRIAR índice &#40;COLUMNSTORE TRANSACT-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql) com REBUILD.  
  
-   [DROP INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
### <a name="clustered-columnstore-indexes"></a>Índices Columnstore clusterizados  
 Para tarefas comuns, consulte [usando índices Columnstore clusterizados](../../database-engine/using-clustered-columnstore-indexes.md).  
  
-   [CRIAR índice &#40;COLUMNSTORE clusterizado TRANSACT-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql) com recompilação ou reorganização.  
  
-   [DROP INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
-   [INSERIR &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
-   [ATUALIZAR &#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
-   [EXCLUIR &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)  
  
### <a name="metadata"></a>los  
 Todas as colunas em um índice columnstore são armazenadas nos metadados como colunas incluídas. O índice columnstore não tem colunas de chave.  
  
-   [o Transact- &#40;SQL sys. Indexes&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
-   [o Transact- &#40;SQL sys. index_columns&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)  
  
-   [o Transact- &#40;SQL sys. partitions&#41;](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql)  
  
-   [o Transact- &#40;SQL sys. column_store_segments&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-segments-transact-sql)  
  
-   [o Transact- &#40;SQL sys. column_store_dictionaries&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql)  
  
-   [o Transact- &#40;SQL sys. column_store_row_groups&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)  
  
  
