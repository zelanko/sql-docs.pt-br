---
title: "Índices columnstore – diretrizes de design | Microsoft Docs"
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc3e22c2-3165-4ac9-87e3-bf27219c820f
caps.latest.revision: 16
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b60c6ab2bc24a2865d06c949a0bb5b765fdc7454
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="columnstore-indexes---design-guidance"></a>Índices columnstore – diretrizes de design
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Recomendações de alto nível para criação de índices columnstore. Poucas boas decisões ajudam a alcançar uma compactação de dados e desempenho de consultas altos que os índices columnstore foram criados para oferecer. 

## <a name="prerequisites"></a>Pré-requisitos

Este artigo pressupõe que você esteja familiarizado com a terminologia e a arquitetura columnstore. Para obter mais informações, consulte [Columnstore indexes – overview (Índices columnstore – visão geral)](../../relational-databases/indexes/columnstore-indexes-overview.md) e [Columnstore indexes – architecture (Índices columnstore – arquitetura)](../../relational-databases/indexes/columnstore-indexes-architecture.md).

### <a name="know-your-data-requirements"></a>Conheça seus requisitos de dados
Antes de criar um índice columnstore, entenda o máximo possível sobre seus requisitos de dados. Por exemplo, pense nas respostas para estas perguntas:

- Quão grande é a minha tabela?
- Na maioria das vezes, as minhas consultas realizam análises que verificam grandes intervalos de valores?  Índices columnstore são criados para funcionar bem para verificações de grandes intervalos em vez de pesquisar valores específicos.
- Minha carga de trabalho realiza muitas atualizações e exclusões? Índices columnstore funcionam bem quando os dados estão estáveis. As consultas devem atualizar e excluir menos de 10% das linhas.
- Eu tenho tabelas de fatos e de dimensões para um data warehouse?
- É necessário executar análise em uma carga de trabalho transacional? Se for o caso, consulte as diretrizes de design columnstore para análises operacionais em tempo real.

Talvez não seja necessário um índice columnstore. Tabelas rowstore com heaps ou índices clusterizados têm melhor desempenho em consultas que buscam nos dados, procurando um valor específico ou para consultas em um pequeno intervalo de valores. Use índices rowstore com cargas de trabalho transacionais, pois eles geralmente tendem a exigir buscas de tabela em vez de verificações de tabela em grandes intervalos.  

## <a name="choose-the-best-columnstore-index-for-your-needs"></a>Escolher o melhor índice columnstore para suas necessidades

Um índice columnstore é clusterizado ou não clusterizado.  Um índice columnstore clusterizado pode ter um ou mais índices btree não clusterizados. Os índices columnstore são mais fáceis de experimentar. Se você criar uma tabela como um índice columnstore, será possível converter facilmente a tabela de volta para uma tabela rowstore removendo o índice columnstore. 

Abaixo, há um resumo das opções e recomendações. 

| Opção columnstore | Recomendações para quando usar | Compactação |
| :----------------- | :------------------- | :---------- |
| Índice columnstore clusterizado | Use para:<br></br>1) Carga de trabalho de data warehouse tradicional com uma estrela ou esquema floco de neve<br></br>2) Cargas de trabalho IOT (Internet das Coisas) que inserem grandes volumes de dados com o mínimo de atualizações e exclusões. | Média de 10 vezes |
| Índices btree não clusterizados em um índice columnstore clusterizado | Use para:<br></br>    1) Impor uma chave primária e restrições de chaves estrangeiras em um índice columnstore clusterizado.<br></br>    2) Acelerar consultas que pesquisam valores específicos ou pequenos intervalos de valores.<br></br>    3) Acelerar atualizações e exclusões de linhas específicos.| Em média, 10x mais um pouco de armazenamento adicional para os NCIs.|
| Índice columnstore não clusterizado em um índice btree ou de heap baseado em disco | Use para: <br></br>1) Uma carga de trabalho OLTP que tem algumas consultas de análise. É possível remover índices btree criados para análise e substituí-los por um índice columnstore não clusterizado.<br></br>2) Muitas cargas de trabalho OLTP tradicionais que realizam operações ETL (Extração, Transformação e Carregamento) para mover dados para um data warehouse separado. É possível eliminar a ETL e um data warehouse separado, criando um índice columnstore não clusterizado em algumas tabelas OLTP. | O NCCI é um índice adicional que requer, em média, 10% a mais de armazenamento.|
| Índice columnstore em uma tabela na memória | As mesmas recomendações que o índice columnstore não clusterizado em uma tabela baseada em disco, a menos que a tabela base seja uma tabela na memória. | O índice columnstore é um índice adicional.|


## <a name="use-a-clustered-columnstore-index-for-large-data-warehouse-tables"></a>Usar um índice columnstore clusterizado para grandes tabelas de data warehouse
O índice columnstore clusterizado é mais do que um índice, ele é o armazenamento de tabela primário. Ele alcança uma alta compactação de dados e uma melhoria significativa no desempenho de consultas em grandes tabelas de fatos e de dimensões de data warehouse. Índices columnstore clusterizados são mais adequados para consultas de análise em vez de consultas transacionais, já que as consultas de análise tendem a realizar operações em grandes intervalos de valores em vez de pesquisar valores específicos. 

Considere usar um índice columnstore clusterizado quando:

- Cada partição tiver pelo menos um milhão de linhas. Índices columnstore tiver rowgroups dentro de cada partição. Se a tabela for muito pequena para preencher um rowgroup em cada partição, você não terá os benefícios da compactação columnstore e do desempenho de consultas.
- As consultas realizam principalmente análises em intervalos de valores. Por exemplo, para localizar o valor médio de uma coluna, a consulta precisa examinar todos os valores de coluna. Em seguida, ele agrega os valores somando-os para determinar a média.
- A maioria das inserções se dão em grandes volumes de dados com o mínimo de atualizações e de exclusões. Muitas cargas de trabalho como IOT (Internet das Coisas) inserem grandes volumes de dados com o mínimo de atualizações e exclusões. Essas cargas de trabalho podem se beneficiar da compactação e de ganhos de desempenho de consultas oriundos do uso de um índice columnstore clusterizado.

Não use um índice columnstore clusterizado quando:

* A tabela exigir tipos de dados varchar(max), nvarchar(max) ou varbinary(max). Ou crie o índice columnstore para que ele não inclua essas colunas.
* Os dados da tabela não são permanentes. Considere usar uma tabela de heap ou temporária quando você precisar armazenar e excluir os dados rapidamente.
* A tabela tiver menos de um milhão de linhas por partição. 
* Mais de 10% das operações na tabela são atualizações e exclusões. Grande número de atualizações e exclusões causam fragmentação. A fragmentação afeta as taxas de compactação e o desempenho de consultas até você executar uma operação chamada reorganizar que força todos os dados para o columnstore e remove a fragmentação. Para obter mais informações, consulte [Minimizing index fragmentation in columnstore indexes (Minimizando a fragmentação de índice nos índices columnstore)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/).

Para obter mais informações, consulte [Columnstore indexes – data warehousing (Índices columnstore – data warehouse)](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md).

## <a name="add-btree-nonclustered-indexes-for-efficient-table-seeks"></a>Adicionar índices btree não clusterizados para buscas de tabela eficientes

A partir do SQL Server 2016, é possível criar índices btree não clusterizados como índices secundários em um índice columnstore clusterizado. O índice btree não clusterizado será atualizado conforme ocorrerem mudanças no índice columnstore. Esse é um recurso avançado que você pode a seu favor. 

Usando o índice btree secundário, é possível pesquisar com eficiência linhas específicas sem examinar todas as linhas.  Outras opções também são disponibilizadas. Por exemplo, é possível impor uma restrição de chave primária ou estrangeira usando uma restrição UNIQUE no índice btree. Como um valor não exclusivo não poderá ser inserido no índice btree, o SQL Server não pode inserir o valor no columnstore. 

Considere usar um índice btree em um índice columnstore para:
* Executar consultas que pesquisam valores específicos ou pequenos intervalos de valores.
* Impor uma restrição como uma chave primária ou restrição de chave estrangeira.
* Realizar operações de atualização e exclusão de maneira eficiente. O índice btree é capaz de localizar rapidamente as linhas específicas para atualizações e exclusões sem verificar toda a tabela ou a partição de uma tabela.
* Você tem armazenamento adicional disponível para armazenar o índice btree.

## <a name="use-a-nonclustered-columnstore-index-for-real-time-analytics"></a>Usar um índice columnstore não clusterizado para análise em tempo real

A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], é possível ter um índice columnstore não clusterizado em uma tabela rowstore baseada em disco ou uma tabela OLTP in-memory. Isso possibilita executar a análise em tempo real em uma tabela transacional. Enquanto as transações estão ocorrendo na tabela subjacente, é possível executar a análise no índice columnstore. Como uma tabela gerencia os índices, as alterações estão disponíveis em tempo real para índices rowstore e columnstore.

Como um índice columnstore tem uma compactação de dados 10x melhor do que um índice rowstore, ele só precisa de uma pequena quantidade de armazenamento extra. Por exemplo, se a tabela rowstore compactada usa 20 GB, o índice columnstore talvez requeira um adicional de 2 GB. O espaço adicional necessário também depende do número de colunas no índice columnstore não clusterizado. 

 Considere usar um índice columnstore não clusterizado para:

* Executar análise em tempo real em uma tabela rowstore transacional. É possível substituir os índices btree existentes desenvolvidos para análises por um índice columnstore não clusterizado. 
  
*   Acabe com a necessidade de ter um data warehouse separado. Normalmente, as empresas executam transações em uma tabela rowstore e, em seguida, carregam os dados em um data warehouse separado para executar a análise. Para muitas cargas de trabalho, é possível eliminar o processo de carregamento e o data warehouse separado criando um índice columnstore não clusterizado em tabelas transacionais.

  O SQL Server 2016 oferece várias estratégias para dar a esse cenário um bom desempenho. É muito fácil experimentá-lo, pois é possível habilitar um índice columnstore não clusterizado sem alterações para seu aplicativo OLTP. 

Para adicionar recursos adicionais de processamento, é possível executar a análise em um secundário legível. Usar um secundário legível separa o processamento da carga de trabalho transacional e a carga de trabalho de análise. 

Para obter mais informações, consulte [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

Para obter mais informações sobre como escolher o melhor índice columnstore, consulte o blog de Sunil Agarwal [Which columnstore index is right for my workload? (Qual índice columnstore é o certo para a minha carga de trabalho?)](https://blogs.msdn.microsoft.com/sql_server_team/columnstore-index-which-columnstore-index-is-right-for-my-workload).

## <a name="use-table-partitions-for-data-management-and-query-performance"></a>Usar partições de tabela para gerenciamento de dados e desempenho de consultas
Os índices columnstore dão suporte ao particionamento, que é uma boa maneira de gerenciar e arquivar dados. O particionamento também melhora o desempenho de consultas limitando operações para uma ou mais partições.

### <a name="use-partitions-to-make-the-data-easier-to-manage"></a>Usar partições para tornar os dados mais fáceis de gerenciar
Para grandes tabelas, a única maneira prática de gerenciar intervalos de dados é usando partições. As vantagens de partições para tabelas rowstore também se aplicam a índices columnstore. 

Por exemplo, tabelas rowstore e columnstore usam partições para:

- Controlar o tamanho de backups incrementais. É possível fazer backup de partições para separar grupos de arquivos e marcá-los como somente leitura. Fazendo isso, os backups futuros ignorarão os grupos de arquivos somente leitura. 
- Economizar custos de armazenamento movendo uma partição mais antiga para um armazenamento mais barato. Por exemplo, você poderia usar a alternância de partição para mover uma partição para um local de armazenamento mais barato.
- Realizar operações com eficiência, limitando as operações a uma partição. Por exemplo, é possível definir como destino apenas as partições fragmentadas para manutenção de índice.

Além disso, com um índice columnstore, use o particionamento para:

* Economizar mais 30% nos custos de armazenamento. É possível compactar as partições mais antigas com as opções de compactação COLUMNSTORE_ARCHIVE. Os dados serão mais lentos para desempenho de consultas. Isso será aceitável se a partição for consultada raramente.

### <a name="use-partitions-to-improve-query-performance"></a>Usar partições para melhorar o desempenho de consultas

Usando partições, é possível limitar suas consultas para examinar somente partições específicas que limita o número de linhas a serem examinadas. Por exemplo, se o índice for particionado por ano e a consulta estiver analisando dados do ano passado, será necessário verificar apenas os dados em uma partição. 

### <a name="use-fewer-partitions-for-a-columnstore-index"></a>Usar menos partições para um índice columnstore

A menos que você tenha um tamanho de dados grande o suficiente, um índice columnstore funciona melhor com partições menores do que a que você poderia usar para um índice rowstore. Se você não tiver pelo menos um milhão de linhas por partição, a maioria de suas linhas poderá ir para o deltastore em que elas não receberão o benefício da compactação columnstore. Por exemplo, se você carregar um milhão de linhas em uma tabela com 10 partições e cada partição receber 100.000 linhas, todas as linhas irão para rowgroups delta. 

Exemplo:
* Carregue 1.000.000 de linhas em uma partição ou em uma tabela não particionada. Você obtém um rowgroup compactado com 1.000.000 de linhas. Isso é ótimo para alta compactação de dados e rápido desempenho de consultas.
* Carregue 1.000.000 de linhas uniformemente em 10 partições. Cada partição recebe 100.000 linhas que é menor que o limite mínimo de compactação columnstore. Como resultado, o índice columnstore poderia ter 10 rowgroups delta com 100.000 linhas em cada. Há maneiras de forçar os rowgroups delta no columnstore. No entanto, se essas forem as únicas linhas no índice columnstore, os rowgroups compactados serão muito pequenos para se ter melhores desempenho de consultas e compactação.

Para obter mais informações sobre particionamento, consulte a postagem do blog de Sunil Agarwal, [Should I partition my columnstore index? (Devo particionar meu índice columnstore?)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-should-i-partition-my-columnstore-index/).

## <a name="choose-the-appropriate-data-compression-method"></a>Escolher o método adequado de compactação de dados
O índice columnstore oferece duas opções de compactação de dados: compactação columnstore e compactação de arquivamento. É possível escolher a opção de compactação quando você cria o índice ou alterá-la posteriormente com [ALTER INDEX... REBUILD](../../t-sql/statements/alter-index-transact-sql.md).

### <a name="use-columnstore-compression-for-best-query-performance"></a>Usar a compactação columnstore para obter melhor desempenho de consultas
Normalmente, a compactação columnstore oferece taxas de compactação 10x melhores em índices rowstore. É o método de compactação padrão para índices columnstore e permite um rápido desempenho de consultas. 

### <a name="use-archive-compression-for-best-data-compression"></a>Usar a compactação de arquivamento para obter melhor compactação de dados
A compactação de arquivamento foi criada para oferecer máxima compactação quando o desempenho de consultas não é tão importante. Ela oferece taxas de compactação de dados maiores do que a compactação columnstore, mas ela tem um porém. Ela leva mais tempo para compactar e descompactar os dados. Portanto, não é adequada para um rápido desempenho de consultas. 

## <a name="use-optimizations-when-you-convert-a-rowstore-table-to-a-columnstore-index"></a>Usar otimizações ao converter uma tabela rowstore em um índice columnstore

Se seus dados já estiverem em uma tabela rowstore, será possível usar [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md) para converter a tabela em um índice columnstore clusterizado. Há algumas otimizações que melhorarão o desempenho de consultas depois que a tabela for convertida.

### <a name="use-maxdop-to-improve-rowgroup-quality"></a>Use MAXDOP para melhorar a qualidade rowgroup
É possível configurar o número máximo de processadores para converter um índice heap ou btree clusterizado em um índice columnstore. Para configurar esses processadores, use o MAXDOP (grau máximo de opção de paralelismo). 

Se você tiver grandes quantidades de dados, o MAXDOP 1 provavelmente será muito lento.  Aumentar o MAXDOP para 4 é conveniente. Se isso resultar em alguns rowgroups que não têm o número ideal de linhas, será possível executar [ALTER INDEX REORG](../../t-sql/statements/alter-index-transact-sql.md) para mesclá-los em segundo plano.

### <a name="keep-the-sorted-order-of-a-btree-index"></a>Manter a ordem de classificação de um índice btree
Como o índice btree já armazena linhas em uma ordem de classificação, preservar essa ordem quando as linhas são compactadas em um índice columnstore pode melhorar o desempenho de consultas.

O índice columnstore não classifica os dados, mas usa metadados para controlar os valores mínimo e máximo de cada segmento de coluna em cada rowgroup.  Ao examinar um intervalo de valores, é possível calcular rapidamente quando ignorar o rowgroup. Quando os dados estão ordenados, mais rowgroups podem ser ignorados. 

Para preservar a ordem de classificação durante a conversão:
* Use [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md) com a cláusula DROP_EXISTING. Isso também preserva o nome do índice. Se você tiver scripts que já usam o nome do índice rowstore, não será necessário atualizá-los. 

    Este exemplo converte um índice rowstore clusterizado em uma tabela chamada ```MyFactTable``` em um índice columnstore clusterizado. O nome do índice, ```ClusteredIndex_d473567f7ea04d7aafcac5364c241e09```, permanece o mesmo.

    ```sql
    CREATE CLUSTERED COLUMNSTORE INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    ON MyFactTable  
    WITH DROP_EXISTING = ON;  
    ```

## <a name="related-tasks"></a>Tarefas relacionadas  
Essas tarefas são destinadas a criar e a manter índices columnstore. 
  
|Tarefa|Tópicos de referência|Observações|  
|----------|----------------------|-----------|  
|Crie uma tabela como columnstore.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar a tabela como um índice columnstore clusterizado. Não é preciso criar primeiro uma tabela rowstore e convertê-la em columnstore.|  
|Crie uma tabela de memória com um índice columnstore.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar uma tabela com otimização na memória com um índice columnstore. O índice columnstore também pode ser adicionado após a criação da tabela, usando a sintaxe ALTER TABLE ADD INDEX.|  
|Converta uma tabela rowstore em columnstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Converta uma pilha ou árvore binária existente em columnstore. Exemplos mostram como lidar com os índices existentes e o nome do índice ao realizar essa conversão.|  
|Converta uma tabela columnstore em rowstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Geralmente, isso não é necessário, mas pode haver ocasiões em que você precisa para realizar essa conversão. Exemplos mostram como converter um columnstore em uma pilha ou um índice clusterizado.|  
|Crie um índice columnstore em uma tabela rowstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Uma tabela rowstore pode ter um índice columnstore.  Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o índice columnstore pode ter uma condição filtrada. Exemplos mostram a sintaxe básica.|  
|Crie índices de alto desempenho para análises operacionais.|[Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|Descreve como criar índices de árvore B e columnstore complementares para que consultas OLTP usem índices de árvore B e consultas de análise usem índices columnstore.|  
|Crie índices columnstore de alto desempenho para data warehouse.|[Índices columnstore – data warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Descreve como usar índices de árvore B em tabelas columnstore para criar consultas de data warehouse de alto desempenho.|  
|Use um índice de árvore B para impor uma restrição de chave primária em um índice columnstore.|[Índices columnstore – data warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Mostra como combinar índices columnstore e de árvore B para impor restrições de chave primária no índice columnstore.|  
|Remover um índice columnstore|[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)|A remoção de um índice columnstore usa a sintaxe DROP INDEX padrão usada pelos índices de árvore B. Remover um índice columnstore clusterizado converterá a tabela columnstore em uma pilha.|  
|Excluir uma linha de um índice columnstore|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Use [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) para excluir uma linha.<br /><br /> **linha columnstore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca a linha como excluída logicamente, mas não recupera o armazenamento físico da linha até que o índice seja recriado.<br /><br /> **linha deltastore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui a linha lógica e fisicamente.|  
|Atualizar uma linha no índice columnstore|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|Use [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) para atualizar uma linha.<br /><br /> **linha columnstore** :  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca a linha como excluída logicamente e insere a linha atualizada no deltastore.<br /><br /> **linha deltastore** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualiza a linha no deltastore.|  
|Força todas as linhas no deltastore a ir para o columnstore.|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) ... REBUILD<br /><br /> [Índices columnstore – desfragmentação](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)|ALTER INDEX com a opção REBUILD força todas as linhas a ir para o columnstore.|  
|Desfragmentar um índice columnstore|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)|ALTER INDEX … REORGANIZE desfragmenta os índices columnstore online.|  
|Mescle tabelas com índices columnstore.|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)|


## <a name="next-steps"></a>Próximas etapas
Para criar um índice columnstore vazio para:

* SQL Server, use [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)
* Banco de Dados SQL, use [CREATE TABLE no Banco de Dados SQL do Azure](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)
* SQL Data Warehouse, use [CREATE TABLE (SQL Data Warehouse do Azure)](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)

Para converter um índice heap ou btree rowstore existente em um índice columnstore clusterizado ou para criar um índice columnstore não clusterizado, use:

* [CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)







  


