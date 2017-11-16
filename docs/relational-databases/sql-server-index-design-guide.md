---
title: "Guia de design de índice do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index design guide
- guide, index design
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: "3"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b164852d30165935ad3b7ce038df1ae07aef3430
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-index-design-guide"></a>Guia de criação de índice do SQL Server
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

Os índices criados inadequadamente e a falta de índices são as principais fontes de afunilamentos do aplicativo de banco de dados. A criação eficiente de índices é muito importante para alcançar um bom desempenho de banco de dados e de aplicativo. Este guia de criação de índice do SQL Server contém informações e práticas recomendadas para ajudar você a criar índices efetivos para atender às necessidades de seu aplicativo.  
    
Este guia presume que o leitor tenha uma compreensão geral dos tipos de índices disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma descrição geral dos tipos de índices, consulte [Tipos de índice](http://msdn.microsoft.com/library/ms175049.aspx).  
  
  
##  <a name="Basics"></a> Noções básicas sobre criação de índice  
 Um índice é uma estrutura em disco associada a uma tabela ou exibição, que agiliza a recuperação das linhas de uma tabela ou exibição. Um índice contém chaves criadas de uma ou mais colunas da tabela ou exibição. Essas chaves são armazenadas em uma estrutura (árvore B) que habilita o SQL Server a localizar a linha ou as linhas associadas aos valores de chave de forma rápida e eficaz.  
  
 A seleção dos índices certos para um banco de dados e sua carga de trabalho é um ato de balanceamento complexo entre a velocidade de consulta e o custo de atualização. Índices limitados ou com poucas colunas na chave de índice exigem menos espaço em disco e sobrecarga de manutenção. Por outro lado, índices amplos cobrem mais consultas. Talvez você precise experimentar vários projetos diferentes antes de encontrar o índice mais eficiente. Os índices podem ser adicionados, modificados e descartados sem afetar o esquema de banco de dados ou o design do aplicativo. Portanto, você não deve hesitar em experimentar índices diferentes.  
  
 O otimizador de consulta no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] escolhe o índice mais eficaz de forma confiável na grande maioria dos casos. Sua estratégia geral de criação de índice deveria fornecer uma variedade de opções de índices para o otimizador de consulta escolher e confiar durante a tomada de decisão correta. Isso reduz o tempo de análise e atinge um bom desempenho em várias situações. Para consultar quais índices o otimizador de consulta usa em uma consulta específica, no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], no menu **Consulta** , selecione **Incluir Plano de Execução Real**.  
  
 Não equipare sempre o uso de índice com bom desempenho e bom desempenho com uso de índice eficiente. Se o uso de um índice sempre ajudasse a produzir o melhor desempenho, a tarefa do otimizador de consulta seria simples. Na realidade, a escolha incorreta de um índice pode causar um desempenho insatisfatório. Portanto, a tarefa do otimizador de consulta é selecionar um índice ou uma combinação de índices apenas quando isso gerar melhoria de desempenho e evitar a recuperação indexada quando isso atrapalhar o desempenho.  
  
### <a name="index-design-tasks"></a>Tarefas de criação de índice  
 As seguintes tarefas compõem a estratégia recomendada para criação de índices:  
  
1.  Entenda as características do banco de dados. Por exemplo, trata-se de um banco de dados OLTP (transação online) com modificações frequentes de dados, um DSS (sistema de apoio à decisão) ou um banco de dados OLAP de data warehouse que contém principalmente dados somente leitura e deve processar conjuntos de dados muito grandes rapidamente. No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], o *columnstore xVelocity de memória otimizada* é especialmente apropriado para conjuntos de dados de data warehouse típicos. Os índices columnstore podem transformar a experiência com data warehouse para usuários proporcionando um desempenho mais rápido para consultas de data warehouse comuns, como filtragem, agregação, agrupamento ou consultas de junção em estrela. Para saber mais, consulte [Guia de índices columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md).  
  
2.  Entenda as características das consultas mais usadas. Por exemplo, saber que uma consulta usada frequentemente associa duas ou mais tabelas o ajudará a determinar o melhor tipo de índice a ser usado.  
  
3.  Entenda as características das colunas usadas nas consultas. Por exemplo, um índice é ideal para colunas que tenham um tipo de dados de inteiro e, também, colunas exclusivas ou não nulas. Para colunas que têm subconjuntos bem definido de dados, é possível usar um índice filtrado no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versões posteriores. Para obter mais informações, consulte [Diretrizes de criação de índice filtrado](#Filtered) neste guia.  
  
4.  Determine quais opções de índice poderiam aumentar o desempenho na criação ou manutenção do índice. Por exemplo, a criação de um índice clusterizado em uma tabela grande existente se beneficiaria da opção de índice ONLINE. A opção ONLINE permite que atividade simultânea nos dados subjacentes continue enquanto o índice está sendo criado ou reconstruído. Para obter mais informações sobre opções de índice, consulte [Definir opções de índice](../relational-databases/indexes/set-index-options.md).  
  
5.  Determine o melhor local de armazenamento para o índice. Um índice não clusterizado pode ser armazenado no mesmo grupo de arquivos que a tabela subjacente ou em um grupo de arquivos diferente. O local de armazenamento de índices pode melhorar o desempenho de consulta aumentando desempenho de E/S do disco. Por exemplo, o armazenamento de um índice não clusterizado em um grupo de arquivos que está em um disco diferente do grupo de arquivos de tabela pode melhorar o desempenho porque vários discos podem ser lidos ao mesmo tempo.  
  
     Alternativamente, os índices clusterizados e não clusterizados podem usar um esquema de partição em vários grupos de arquivos. O particionamento facilita o gerenciamento de tabelas ou índices grandes permitindo o acesso ou o gerenciamento de subconjuntos de dados de forma rápida e eficaz, enquanto mantém a integridade geral da coleção. Para obter mais informações, consulte [Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md). Quando você pensar em particionamento, determine se o índice deve ser alinhado; isto é, particionado essencialmente da mesma maneira que a tabela ou particionado de forma independente.  
  
##  <a name="General_Design"></a> Diretrizes para criação de índice geral  
 Administradores de banco de dados experientes podem projetar um bom conjunto de índices, mas essa tarefa é muito complexa, demorada e propensa a erros até mesmo para bancos de dados e cargas de trabalho moderadamente complexos. Compreender as características de seu banco de dados, consultas e colunas de dados pode lhe ajudar a projetar índices melhores.  
  
### <a name="database-considerations"></a>Considerações sobre banco de dados  
 Quando você projeta um índice, considere as seguintes diretrizes para banco de dados:  
  
-   Números grandes de índices em uma tabela afetam o desempenho das instruções INSERT, UPDATE, DELETE e MERGE porque todos os índices precisam ser ajustados adequadamente à medida que os dados são alterados em uma tabela. Por exemplo, se uma coluna for usada em vários índices e você executar uma instrução UPDATE que modifica os dados dessa coluna, cada índice que contém essa coluna deverá ser atualizado, bem como a coluna na tabela base subjacente (heap ou índice clusterizado).  
  
    -   Evite tabelas fortemente atualizadas em cima desindexações e mantenha os índices estreitos, ou seja, com o mínimo de colunas possível.  
  
    -   Use muitos índices para aperfeiçoar o desempenho da consulta em tabelas com baixos requisitos de atualização, mas com grandes volumes de dados. Grandes números de índices podem ajudar o desempenho de consultas que não modificam dados, como instruções SELECT, porque o otimizador de consulta tem mais índices para escolher para determinar o método de acesso mais rápido.  
  
-   Indexar tabelas pequenas pode não ser bom porque pode fazer o otimizador de consulta levar mais tempo para atravessar o índice procurando dados do que executar uma simples varredura de tabela. Portanto, os índices em tabelas pequenas talvez nunca sejam usados, mas ainda devem ser mantidos como dados nas alterações de tabela.  
  
-   Índices em exibições pode prover ganhos de desempenho significantes quando a exibição contiver agregações, junções de tabela ou uma combinação de agregações e junções. A exibição não precisa estar explicitamente referenciada na consulta para o otimizador de consulta usá-la.  
  
-   Use o Orientador de Otimização do Mecanismo de Banco de Dados para analisar seu banco de dados e fazer recomendações de índice. Para obter mais informações, consulte [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md).  
  
### <a name="query-considerations"></a>Considerações sobre consultas  
 Quando você projeta um índice, considere as seguintes diretrizes para consultas:  
  
-   Crie índices não clusterizados nas colunas frequentemente usadas em predicados e condições de junção em consultas. No entanto, evite adicionar colunas desnecessárias. Acrescentar muitas colunas de índice pode afetar adversamente o espaço em disco e o desempenho de manutenção de índice.  
  
-   Cobrindo índices pode melhorar desempenho de consulta porque todos os dados precisaram satisfazer os requisitos da consulta existe dentro do próprio índice. Ou seja, apenas as páginas de índice, e não as páginas de dados da tabela ou do índice clusterizado, são necessárias para recuperar os dados solicitados, portanto reduzindo as operações de E/S gerais do disco. Por exemplo, uma consulta de colunas **a** e **b** em uma tabela que tem um índice composto criado em colunas **a**, **b**e **c** pode recuperar os dados especificados somente do índice.  
  
-   Escreva consultas que insiram ou modifiquem o máximo de filas possível em uma única instrução, em vez de usar consultas múltiplas para atualizar essas mesmas filas. Ao usar apenas uma instrução, pode-se explorar uma manutenção otimizada do índice.  
  
-   Avalie o tipo da consulta e como as colunas são usadas na consulta. Por exemplo, uma coluna usada em uma consulta de correspondência exata seria uma boa candidata para um índice clusterizado ou não clusterizado.
  
### <a name="column-considerations"></a>Considerações sobre colunas  
 Quando você projeta um índice, considere as seguintes diretrizes para as colunas:  
  
-   Mantenha o comprimento da chave de índice curto para os índices clusterizados. Além disso, os índices clusterizados se beneficiam de serem criados em colunas exclusivas ou não nulas.  
  
-   Colunas que são dos tipos de dados **ntext**, **text**, **image**, **varchar(max)**, **nvarchar(max)**e **varbinary(max)** não podem ser especificadas como colunas de chave de índice. Entretanto, os tipos de dados **varchar(max)**, **nvarchar(max)**, **varbinary(max)**e **xml** podem participar de um índice não clusterizado, como colunas de índice não chave. Para obter mais informações, consulte a seção ['Índice com colunas incluídas](#Included_Columns)' neste guia.  
  
-   Um tipo de dados **xml** só pode ser uma coluna de chave em um índice XML. Para obter mais informações, consulte [Índices XML &#40;SQL Server&#41;](../relational-databases/xml/xml-indexes-sql-server.md). O SQL Server 2012 SP1 apresenta um novo tipo de índice XML conhecido como um índice XML seletivo. Esse novo índice pode melhorar o desempenho da consulta dos dados armazenados como XML no SQL Server, permitir uma indexação muito mais rápida de cargas de trabalho de dados XML grandes e melhorar a escalabilidade ao reduzir os custos de armazenamento do próprio índice. Para obter mais informações, consulte [Índices XML seletivos &#40;SXI&#41;](../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
-   Examine a singularidade da coluna. Um índice exclusivo em vez de um índice não exclusivo na mesma combinação de colunas, provê informações adicional para o otimizador de consulta, o que torna o índice mais útil. Para obter mais informações, consulte [Diretrizes de design de índice exclusivo](#Unique) neste guia.  
  
-   Examine a distribuição de dados na coluna. Frequentemente, uma consulta longa é causada ao se indexar uma coluna com poucos valores exclusivos, ou ao executar uma junção em tal coluna. Isto é um problema fundamental com dados e consulta, e geralmente não pode ser resolvido sem identificar esta situação. Por exemplo, uma lista telefônica física ordenada alfabeticamente pelo último nome não será rápida em localizar uma pessoa, se todas as pessoas na cidade tiverem nomes de Smith ou Jones. Para obter mais informações sobre distribuição de dados, consulte [Statistics](../relational-databases/statistics/statistics.md).  
  
-   Considere o uso de índices filtrados em colunas com subconjuntos bem definidos, por exemplo, colunas esparsas, colunas com grande a maioria dos valores NULL, colunas com categorias de valores e colunas com intervalos diferentes de valores. Um índice filtrado bem projetado pode melhorar o desempenho da consulta e reduzir os custos de manutenção de índice e de armazenamento.  
  
-   Considere a ordem das colunas se o índice contiver colunas múltiplas. A coluna que é usada na cláusula WHERE em um critério de consulta igual a (=), maior que (>), menor que (>) ou BETWEEN, ou que participa em uma junção, deve ser posicionada primeiro. Colunas adicionais devem ser ordenadas com base em seu nível de distinção, ou seja, do mais distinto ao menos distinto.  
  
     Por exemplo, se o índice for definido como `LastName`, `FirstName` o índice será útil quando o critério de consulta for `WHERE LastName = 'Smith'` ou `WHERE LastName = Smith AND FirstName LIKE 'J%'`. Porém, o otimizador de consulta não usaria o índice para uma consulta que tivesse pesquisado apenas em `FirstName (WHERE FirstName = 'Jane')`.  
  
-   Considere indexar as colunas computadas. Para obter mais informações, consulte [Indexes on Computed Columns](../relational-databases/indexes/indexes-on-computed-columns.md).  
  
### <a name="index-characteristics"></a>Características do índice  
 Depois de ter determinado que um índice é apropriado para uma consulta, você pode selecionar o tipo de índice que melhor se adéque a sua situação. Características de índice incluem o seguinte:  
  
-   Clusterizado X não clusterizado.  
  
-   Exclusivo X não exclusivo  
  
-   Única coluna X multicoluna  
  
-   Ordem crescente ou decrescente em colunas no índice  
  
-   Tabela completa versus filtrada para índices não clusterizados  
  
 Você também pode personalizar as características de armazenamento inicial do índice para aperfeiçoar seu desempenho ou manutenção definindo uma opção como FILLFACTOR. Além disso, você pode determinar o local de armazenamento de índice usando grupos de arquivos ou esquemas de partição para aperfeiçoar o desempenho.  
  
###  <a name="Index_placement"></a> Posição do índice em grupos de arquivos ou esquemas de partição  
 À medida que desenvolve sua estratégia de design de índices, considere a colocação dos índices nos grupos de arquivos associados ao banco de dados. A seleção cuidadosa do grupo de arquivos ou esquema de partição pode melhorar o desempenho da consulta.  
  
 Por padrão, os índices são armazenados no mesmo grupo de arquivos que a tabela base na qual o índice é criado. Um índice cluster não particionado e a tabela base sempre residem no mesmo grupo de arquivos. No entanto, você pode fazer o seguinte:  
  
-   Crie índices não clusterizados em um grupo de arquivos diferente do grupo de arquivos da tabela base ou do índice clusterizado.  
  
-   Particione índices cluster e não cluster para que ocupem vários grupos de arquivos.  
  
-   Mova uma tabela de um grupo de arquivos para outro descartando o índice cluster e especificando um novo grupo de arquivos ou esquema de partição na cláusula MOVE TO da instrução DROP INDEX ou usando a instrução CREATE INDEX com a cláusula DROP_EXISTING.  
  
 Ao criar o índice não cluster em um grupo de arquivos diferente, você pode obter ganhos de desempenho se os grupos de arquivos estiverem usando unidades físicas diferentes com seus próprios controladores. As informações de índices e de dados podem ser lidas em paralelo pelas várias cabeças de disco. Por exemplo, se `Table_A` no grupo de arquivos `f1` e `Index_A` no grupo de arquivos `f2` estiverem ambos sendo usados pela mesma consulta, podem-se obter ganhos de desempenho porque os dois grupos de arquivos estão sendo completamente usados sem contenção. Porém, se `Table_A` for verificado pela consulta, mas `Index_A` não for referenciado, apenas o grupo de arquivos `f1` será usado. Isso não cria nenhum ganho de desempenho.  
  
 Como você não pode prever que tipo de acesso acontecerá e quando ocorrerá, pode ser preferível distribuir suas tabelas e índices por todos os grupos de arquivos. Isso garantirá que todos os discos estejam sendo acessados, pois todos os dados e índices estarão distribuídos igualmente por todos os discos, independentemente da maneira como os dados sejam acessados. Essa também é uma abordagem mais simples para os administradores do sistema.  
  
#### <a name="partitions-across-multiple-filegroups"></a>Partições em vários grupos de arquivos  
 Você também pode considerar o particionamento de índices cluster e não cluster em vários grupos de arquivos. Os índices particionados são particionados horizontalmente, ou por linha, com base na função de uma partição. A função da partição define como cada linha é mapeada para um conjunto de partições, com base nos valores de certas colunas, chamadas colunas de particionamento. Um esquema de partição especifica o mapeamento das partições para um conjunto de grupos de arquivos.  
  
 O particionamento de um índice pode proporcionar os seguintes benefícios:  
  
-   Proporcionar sistemas evolutivos que tornam grandes índices mais gerenciáveis. Sistemas OLTP, por exemplo, podem implementar aplicativos que reconhecem partição que tratam de índices grandes.  
  
-   Fazer as consultas serem executadas de maneira mais rápida e eficiente. Quando as consultas acessarem várias partições de um índice, o otimizador de consulta pode processar partições individuais ao mesmo tempo e pode excluir partições que não sejam afetadas pela consulta.  
  
 Para obter mais informações, consulte [Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
###  <a name="Sort_Order"></a> Diretrizes de criação de ordem de classificação de índice  
 Ao definir índices, confirme se os dados da coluna de chave de índice deverão ser armazenados em ordem crescente ou decrescente. Ordem crescente é o padrão e assegura a compatibilidade com as versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A sintaxe das instruções CREATE INDEX, CREATE TABLE e ALTER TABLE dá suporte às palavras-chave ASC (crescente) e DESC (decrescente) em colunas individuais de índices e restrições.  
  
 A especificação da ordem de armazenamento dos valores de chave em um índice é útil quando as consultas que fazem referência à tabela contêm cláusulas ORDER BY que especificam direcionamentos diferentes para a coluna de chave ou as colunas daquele índice. Nesses casos, o índice pode eliminar a necessidade de um operador SORT no plano de consulta, o que torna a consulta mais eficaz. Por exemplo, os compradores do departamento de compras da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] devem avaliar a qualidade dos produtos que adquirem de fornecedores. Os compradores estão mais interessados em localizar os produtos enviados por esses fornecedores, e que têm alta taxa de rejeição. Como demonstrado pela consulta a seguir, recuperar os dados para atender esses critérios requer que a coluna `RejectedQty` da tabela `Purchasing.PurchaseOrderDetail` seja classificada em ordem decrescente (do maior para o menor) e que a coluna `ProductID` seja classificada em ordem crescente (do menor para o maior).  
  
```  
SELECT RejectedQty, ((RejectedQty/OrderQty)*100) AS RejectionRate,  
    ProductID, DueDate  
FROM Purchasing.PurchaseOrderDetail  
ORDER BY RejectedQty DESC, ProductID ASC;  
```  
  
 O plano de execução a seguir, dessa consulta, mostra que o otimizador de consultas usou um operador SORT para retornar o conjunto de resultados na ordem especificada pela cláusula ORDER BY.  
  
 ![IndexSort1](../relational-databases/media/indexsort1.gif)
  
  
 Se um índice for criado com colunas de chave correspondentes às da cláusula ORDER BY da consulta, o operador SORT poderá ser eliminado do plano de consulta, e este se tornará mais eficaz.  
  
```  
CREATE NONCLUSTERED INDEX IX_PurchaseOrderDetail_RejectedQty  
ON Purchasing.PurchaseOrderDetail  
    (RejectedQty DESC, ProductID ASC, DueDate, OrderQty);  
```  
  
 Depois que a consulta for novamente executada, o plano de execução a seguir mostra que o operador SORT foi eliminado e que o índice não clusterizado recentemente criado é utilizado.  
  
 ![InsertSort2](../relational-databases/media/insertsort2.gif)
  
  
 O [!INCLUDE[ssDE](../includes/ssde-md.md)] pode se mover para qualquer direção de forma igualmente eficaz. Um índice definido como `(RejectedQty DESC, ProductID ASC)` ainda pode ser usado em uma consulta na qual a direção de classificação das colunas da cláusula ORDER BY é invertida. Por exemplo, uma consulta com a cláusula ORDER BY `ORDER BY RejectedQty ASC, ProductID DESC` pode utilizar o índice.  
  
 A ordem de classificação só pode ser especificada para colunas de chave. A exibição de catálogo [sys.index_columns](../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md) e a função INDEXKEY_PROPERTY relatam se a coluna de índice está armazenada em ordem crescente ou decrescente.  
  
  
##  <a name="Clustered"></a> Diretrizes de design de índices clusterizados  
 Os índices clusterizados classificam e armazenam as linhas de dados da tabela com base em seus valores de chave. Pode haver apenas um índice clusterizado por tabela, porque as próprias linhas de dados podem ser classificadas apenas em uma única ordem. Com poucas exceções, toda tabela deveria ter um índice clusterizado definido na coluna ou colunas, o qual proporciona o seguinte:  
  
-   Pode ser usado para consultas frequentemente usadas.  
  
-   Oferece um alto grau de singularidade.  
  
    > [!NOTE]  
    >  Quando você cria uma restrição PRIMARY KEY, um índice exclusivo na coluna, ou colunas, é criado automaticamente. Por padrão, esse índice é cluster. Porém, você pode especificar um índice não clusterizado ao criar a restrição.  
  
-   Pode ser usado em consultas de intervalo.  
  
 Se o índice clusterizado não for criado com a propriedade UNIQUE, o [!INCLUDE[ssDE](../includes/ssde-md.md)] acrescentará uma coluna de indicador de exclusividade de 4 bytes automaticamente à tabela. Quando necessário, o [!INCLUDE[ssDE](../includes/ssde-md.md)] acrescenta um valor de indicador de exclusividade automaticamente a uma linha para tornar cada chave exclusiva. Essa coluna e seus valores são usados internamente e não podem ser vistos ou avaliados por usuários.  
  
### <a name="clustered-index-architecture"></a>Arquitetura de índice clusterizado  
 No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], os índices são organizados como árvores B. Cada página em uma árvore B de índice é chamada de nó do índice. O nó superior da árvore B é chamado de nó raiz. Os nós inferiores no índice são chamados de nós folha. Quaisquer níveis de índice entre os nós raiz e folha são coletivamente conhecidos como níveis intermediários. Em um índice clusterizado, os nós folha contêm as páginas de dados da tabela subjacente. Os nós de nível intermediário e raiz contêm páginas de índice com linhas de índice. Cada linha de índice contém um valor de chave e um ponteiro para uma página de nível de intermediário na árvore B ou uma linha de dados no nível folha do índice. As páginas de cada nível do índice são vinculadas a uma lista vinculada duas vezes.  
  
 Índices clusterizados têm uma linha em [sys.partitions](../relational-databases/system-catalog-views/sys-partitions-transact-sql.md), com **index_id** = 1 para cada partição usada pelo índice. Por padrão, um índice clusterizado tem um único particionamento. Quando um índice clusterizado tem particionamentos múltiplos, cada particionamento tem uma estrutura de árvore B que contém os dados para aquele particionamento específico. Por exemplo, se um índice clusterizado tiver quatro particionamentos, haverá quatro estruturas de árvore B; uma em cada particionamento.  
  
 Dependendo dos tipos de dados no índice clusterizado, cada estrutura de índice clusterizado terá uma ou mais unidades de alocação para armazenar e gerenciar os dados de um particionamento específico. No mínimo, cada índice clusterizado terá uma unidade de alocação IN_ROW_DATA por particionamento. O índice clusterizado também terá uma unidade de alocação LOB_DATA por particionamento se contiver colunas LOB (objetos grandes). Também terá uma unidade de alocação ROW_OVERFLOW_DATA por particionamento se tiver colunas de comprimento variável excedendo o limite de tamanho de linha de 8.060 bytes.  
  
 As páginas da cadeia de dados e as linhas são classificadas pelo valor da chave de índice clusterizado. Todas as inserções são feitas no ponto em que o valor de chave da linha inserida se ajusta à sequência de classificação entre as linhas existentes.  
  
 Esta ilustração mostra a estrutura de um índice clusterizado em um único particionamento.  
 
 ![bokind2](../relational-databases/media/bokind2.gif)  
  
### <a name="query-considerations"></a>Considerações sobre consultas  
 Antes de criar índices clusterizados, entenda como seus dados serão acessados. Considere utilizar um índice clusterizado para consultas que façam o seguinte:  
  
-   Retornam um intervalo de valores usando os operadores como BETWEEN, >, >=, < e <=.  
  
     Depois que a linha com o primeiro valor for encontrada usando o índice cluster, garante-se que as linhas com valores indexados subsequentes estejam fisicamente adjacentes. Por exemplo, se uma consulta recuperar registros entre um intervalo de números de ordem de vendas, um índice clusterizado na coluna `SalesOrderNumber` poderá localizar rapidamente a linha que contém o número de ordem de vendas inicial e em seguida recuperará todas as linhas sucessivas na tabela, até que o último número de ordem de vendas seja alcançado.  
  
-   Retornam grandes conjuntos de resultados.  
  
-   Use cláusulas JOIN. Normalmente elas são colunas de chave estrangeira.  
  
-   Use cláusulas ORDER BY ou GROUP BY.  
  
     Um índice nas colunas especificadas na cláusula ORDER BY ou GROUP BY pode eliminar a necessidade de o [!INCLUDE[ssDE](../includes/ssde-md.md)] classificar os dados, pois as linhas já estão classificadas. Isso melhora o desempenho da consulta.  
  
### <a name="column-considerations"></a>Considerações sobre colunas  
 Geralmente, você deve definir a chave de índice clusterizado com o menor número de colunas possível. Considere colunas que tenham um ou mais dos seguintes atributos:  
  
-   Sejam exclusivas ou contenham muitos valores distintos  
  
     Por exemplo, uma ID de funcionário identifica os funcionários de maneira exclusiva. Um índice clusterizado ou restrição PRIMARY KEY na coluna `EmployeeID` melhoraria o desempenho de consultas que pesquisam informações de funcionário com base no número de ID do funcionário. Como alternativa, um índice clusterizado poderia ser criado em `LastName`, `FirstName`, `MiddleName` porque os registros dos funcionários são agrupados e consultados frequentemente dessa maneira e a combinação dessas colunas ainda ofereceria um grau alto de diferença.  
  
-   Sejam acessadas sequencialmente  
  
     Por exemplo, um ID de produto identifica produtos de maneira exclusiva na tabela `Production.Product` no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . Consultas nas quais uma pesquisa sequencial seja especificada, tais como `WHERE ProductID BETWEEN 980 and 999`, se beneficiariam de um índice clusterizado em `ProductID`. Isso ocorre porque as linhas seriam armazenadas em ordem classificada nessa coluna de chave.  
  
-   Definido como IDENTITY.  
  
-   Frequentemente usado para classificar os dados recuperados de uma tabela.  
  
     Pode ser uma boa ideia agrupar, ou seja, classificar fisicamente, a tabela nessa coluna para economizar o custo de uma operação de classificação toda vez que a coluna for consultada.  
  
 Índices clusterizados não são uma boa escolha para os seguintes atributos:  
  
-   Colunas que sofrem mudanças frequentes  
  
     Isso faz com que uma fila inteira se mova, pois o [!INCLUDE[ssDE](../includes/ssde-md.md)] deve manter os valores de dados de uma linha em ordem física. Essa é uma consideração importante em sistemas de processamento de transações de alto volume nos quais os dados sejam normalmente voláteis.  
  
-   Chaves largas  
  
     Chaves largas são uma combinação de várias colunas ou de várias colunas de tamanho grande. Os valores de chave do índice clusterizado são usados por todos os índices não clusterizados como chaves de pesquisa. Qualquer índice não clusterizado definido na mesma tabela será significativamente maior porque as entradas de índice não clusterizado contêm a chave de cluster e também as colunas de chave definidas para aquele índice não clusterizado.  
  
  
##  <a name="Nonclustered"></a> Diretrizes de criação de índice não clusterizado  
 Um índice não clusterizado contém os valores de chave do índice e os localizadores de linha que apontam para o local de armazenamento dos dados da tabela. Você pode criar vários índices não clusterizados em uma tabela ou exibição indexada. Em geral, os índices não clusterizados devem ser criados para aprimorar o desempenho de consultas utilizadas com frequência que não são cobertas pelo índice clusterizado.  
  
 Semelhante à maneira como o índice de um livro é usado, o otimizador de consulta procura um valor de dados pesquisando o índice não clusterizado para encontrar o local do valor de dados na tabela e, depois, recupera os dados diretamente daquele local. Isso faz com que os índices não clusterizados sejam a opção ideal para consultas de correspondência exata, uma vez que o índice contém entradas que descrevem o local preciso na tabela dos valores de dados pesquisados pelas consultas. Por exemplo, para consultar a tabela `HumanResources. Employee` de todos os funcionários que reportam para um determinado gerente, o otimizador de consulta pode usar o índice não clusterizado `IX_Employee_ManagerID`, que tem `ManagerID` como sua coluna de chave. O otimizador de consulta pode localizar rapidamente todas as entradas no índice que correspondem ao `ManagerID`especificado. Cada entrada do índice aponta para a página e a linha exatas na tabela ou índice clusterizado, em que os dados correspondentes podem ser localizados. Depois que o otimizador de consulta localizar todas as entradas no índice, poderá ir diretamente para a página e a linha exatas e recuperar os dados.  
  
### <a name="nonclustered-index-architecture"></a>Arquitetura de índice não clusterizado  
 Os índices não clusterizados têm a mesma estrutura de árvore B que os índices clusterizados, com exceção das seguintes diferenças significativas:  
  
-   As linhas de dados da tabela subjacente não são classificadas nem armazenadas em ordem com base nas suas chaves não clusterizadas.  
  
-   A camada de folha de um índice não clusterizado é constituída de páginas de índice, em vez de páginas de dados.  
  
 Os localizadores de linha, em linhas de índice não clusterizado, são um ponteiro para uma linha ou uma chave de índice clusterizado para uma linha, como descrito a seguir.  
  
-   Se a tabela for um heap, ou seja, se não tiver um índice clusterizado, o localizador de linha será um ponteiro para a linha. O ponteiro é criado a partir do ID (identificador), do número da página e do número da linha na página do arquivo. O ponteiro inteiro é conhecido como RID (Identificação de Linha).  
  
-   Se a tabela tiver um índice clusterizado, ou o índice estiver em uma exibição indexada, o localizador de linha será a chave de índice clusterizado da linha.  
  
 Os índices não clusterizados têm uma linha em [sys.partitions](../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) com **index_id** >1 para cada partição usada pelo índice. Por padrão, um índice não clusterizado tem uma única partição. Quando um índice não clusterizado tem várias partições, cada partição tem uma estrutura de árvore B que contém linhas de índice para aquela partição específica. Por exemplo, se um índice não clusterizado tiver quatro partições, haverá quatro estruturas de árvore B, uma em cada partição.  
  
 Dependendo dos tipos de dados no índice não clusterizado, cada estrutura de índice não clusterizado terá uma ou mais unidades de alocação para armazenar e gerenciar os dados de uma partição específica. No mínimo, cada índice não clusterizado terá uma unidade de alocação IN_ROW_DATA por partição que armazena as páginas de árvore B do índice. O índice não clusterizado também terá uma unidade de alocação LOB_DATA por partição se contiver colunas LOB (objetos grandes). Além disso, terá uma unidade de alocação ROW_OVERFLOW_DATA por partição se contiver colunas de comprimento variável que excedem o limite de tamanho de linha de 8.060 bytes.  
  
 A ilustração a seguir mostra a estrutura de um índice não clusterizado em uma única partição.  

![bokind1a](../relational-databases/media/bokind1a.gif)  
  
  
### <a name="database-considerations"></a>Considerações sobre banco de dados  
 Considere as características do banco de dados ao criar índices não clusterizados.  
  
-   Os bancos de dados ou as tabelas com baixos requisitos de atualização, mas volumes grandes de dados, podem se beneficiar de muitos índices não clusterizados para aprimorar o desempenho da consulta. Considere a criação de índices filtrados para subconjuntos bem definidos de dados para aprimorar o desempenho da consulta, reduzir os custos de armazenamento de índice e reduzir os custos de manutenção de índice comparados a índices não clusterizados de tabela completa.  
  
     Os aplicativos do Sistema de Suporte a Decisões e os bancos de dados que contêm fundamentalmente dados somente leitura podem se beneficiar de vários índices não clusterizados. O otimizador de consulta tem mais índices dos quais selecionar para determinar o método de acesso mais rápido e as baixas características de atualização do banco de dados significam que a manutenção do índice não impedirá o desempenho.  
  
-   Os aplicativos de Processamento de Transações online e os bancos de dados que contêm tabelas com grandes atualizações devem evitar a superindexação. Adicionalmente, os índices deveriam ser restritos, ou seja, com o mínimo possível de colunas.  
  
     Números grandes de índices em uma tabela afetam o desempenho das instruções INSERT, UPDATE, DELETE e MERGE porque todos os índices precisam ser ajustados adequadamente à medida que os dados são alterados em uma tabela.  
  
### <a name="query-considerations"></a>Considerações sobre consultas  
 Antes de criar índices não clusterizados, é recomendado entender como os dados são acessados. Considere usar um índice não clusterizado para consultas com os seguintes atributos:  
  
-   Use as cláusulas JOIN ou GROUP BY.  
  
     Crie vários índices não clusterizados em colunas envolvidas em operações de junção e de agrupamento e um índice clusterizado em qualquer coluna de chave estrangeira.  
  
-   Consultas que não retornam grandes conjuntos de resultados.  
  
     Crie índices filtrados para abranger consultas que retornam um subconjunto bem definido de linhas de uma tabela grande.  
  
-   Contém as colunas envolvidas frequentemente em condições de pesquisa de consulta, como a cláusula WHERE, que retorna correspondências exatas.  
  
### <a name="column-considerations"></a>Considerações sobre colunas  
 Considere as colunas que tenham um ou mais destes atributos:  
  
-   Cubra a consulta.  
  
     São obtidos ganhos de desempenho quando o índice contém todas as colunas da consulta. O otimizador de consulta pode localizar todos os valores da coluna dentro do índice. Os dados de tabela ou de índice clusterizado não são acessados, o que resulta em menos operações de E/S. Use índice com colunas incluídas para adicionar colunas de cobertura, em vez de criar uma ampla chave de índice.  
  
     Se a tabela tiver um índice clusterizado, a coluna ou as colunas definidas no índice clusterizado serão anexadas automaticamente ao final de cada índice não clusterizado da tabela. Isso pode produzir uma consulta coberta sem especificar as colunas de índice clusterizado na definição do índice não clusterizado. Por exemplo, se uma tabela tiver um índice clusterizado na coluna `C`, um índice não clusterizado nas colunas `B` e `A` , terá como colunas de valores de chave `B`, `A`e `C`.  
  
-   Muitos valores distintos, como uma combinação de sobrenome e nome, caso um índice clusterizado seja usado em outras colunas.  
  
     Se houver poucos valores distintos, como apenas 1 e 0, a maioria das consultas não usará o índice porque uma verificação de tabela é, em geral, mais eficaz. Para esse tipo de dados, considere a criação de um índice filtrado em um valor diferente que ocorra apenas em um número pequeno de linhas. Por exemplo, se a maioria dos valores for 0, o otimizador de consulta pode usar um índice filtrado para as linhas de dados que contêm 1.  
  
####  <a name="Included_Columns"></a> Usar colunas incluídas para estender índices não clusterizados  
 Você pode estender a funcionalidade de índices não clusterizados acrescentando colunas de não chave ao nível folha do índice não cluster. Ao incluir colunas não chave, você pode criar você índices não clusterizados que abrangem mais consultas. Isto porque as colunas não chave têm os seguintes benefícios:  
  
-   Elas podem ser tipos de dados não permitidos como colunas de chave de índice.  
  
-   Eles não são considerados pelo [!INCLUDE[ssDE](../includes/ssde-md.md)] ao calcular o número de colunas de chave de índice ou o tamanho da chave de índice.  
  
 Um índice com colunas não chave incluídas pode melhorar o desempenho de consulta significativamente quando todas as colunas na consulta forem incluídas no índice como colunas de chave ou não chave. Os ganhos de desempenho são alcançados pois o otimizador de consulta pode localizar todos os valores de coluna dentro do índice, a tabela, ou dados de índice clusterizado não são acessados, resultando em poucas operações de E/S de disco.  
  
> [!NOTE]  
>  Quando um índice contém todas colunas referenciadas pela consulta, ele costuma ser referenciado como se abrangendo a consulta.  
  
 Enquanto as colunas de chave são armazenadas em todos os níveis do índice, as colunas não chave são armazenadas apenas em nível folha.  
  
##### <a name="using-included-columns-to-avoid-size-limits"></a>Usando colunas incluídas para evitar limites de tamanho  
 Você pode incluir colunas não chave em um índice não clusterizado para evitar exceder as limitações do tamanho atual do índice, de um máximo de 16 colunas de chave, e um máximo de tamanho chave de índice de 900 bytes. O [!INCLUDE[ssDE](../includes/ssde-md.md)] não considera as colunas não chave ao calcular o número de colunas de chave de índice, ou o tamanho da chave do índice.  
  
 Por exemplo, suponha que você quer indexar as colunas seguintes na tabela `Document` :  
  
 `Title nvarchar(50)`  
  
 `Revision nchar(5)`  
  
 `FileName nvarchar(400)`  
  
 Como os tipos de dados **nchar** e **nvarchar** exigem 2 bytes para cada caractere, um índice que contém essas três colunas ultrapassaria a limitação de tamanho de 900 bytes por 10 bytes (455 * 2). Ao usar a cláusula `INCLUDE` da declaração `CREATE INDEX` , a chave de índice pode ser definida como uma coluna não chave (`Title, Revision`) e `FileName` . Desse modo, o tamanho da chave de índice seria de 110 bytes (55 \* 2) e o índice ainda conteria todas as colunas necessárias. A seguinte declaração cria tal índice.  
  
```  
CREATE INDEX IX_Document_Title   
ON Production.Document (Title, Revision)   
INCLUDE (FileName);   
```  
  
##### <a name="index-with-included-columns-guidelines"></a>Índice com diretrizes das colunas incluídas  
 Quando você projeta índices não clusterizados com colunas incluídas, considere as seguintes diretrizes:  
  
-   As colunas não chave estão definidas na cláusula INCLUDE da instrução CREATE INDEX.  
  
-   As colunas não chave só podem ser definidas em índices não clusterizados em tabelas, ou em exibições indexadas.  
  
-   São permitidos todos os tipos de dados, exceto **text**, **ntext**e **image**.  
  
-   As colunas computadas que são determinísticas e precisas ou imprecisas podem ser colunas incluídas. Para obter mais informações, consulte [Indexes on Computed Columns](../relational-databases/indexes/indexes-on-computed-columns.md).  
  
-   Assim como com as colunas de chave, as colunas computadas derivadas dos tipos de dados **image**, **ntext**e **text** podem ser colunas não chave (incluídas), desde que o tipo de dados da coluna computada seja permitido como uma coluna de índice não chave.  
  
-   Os nomes das colunas não podem ser especificados na lista INCLUDE e na lista de coluna de chave.  
  
-   Os nomes das colunas não podem ser repetidos na lista INCLUDE.  
  
##### <a name="column-size-guidelines"></a>Diretrizes do tamanho da coluna  
  
-   Pelo menos uma coluna de chave deve ser definida. O número de máximo de colunas não chave é de 1023 colunas. Esse é o número máximo de colunas de tabela menos 1.  
  
-   As colunas de chave de índice, exceto as não chave, devem seguir as restrições de tamanho de índice de no máximo 16 colunas de chave, e um tamanho total de chave de índice de no máximo 900 bytes.  
  
-   O tamanho total de todas as colunas não chave está limitado somente pelo tamanho especificado das colunas na cláusula INCLUDE; por exemplo, as colunas **varchar(max)** estão limitadas a 2 GB.  
  
##### <a name="column-modification-guidelines"></a>Diretrizes para modificação de coluna  
 Quando você modifica uma coluna de tabela que estava definida como uma coluna incluída, as restrições seguintes se aplicam:  
  
-   As colunas não chave não podem ser soltar das tabelas, a menos que o índice seja solto antes.  
  
-   As colunas não chave não podem ser alteradas, exceto para fazerem o seguinte:  
  
    -   Alterar a nulidade da coluna da coluna NOT NULL até NULL.  
  
    -   Aumente o tamanho das colunas **varchar**, **nvarchar**ou **varbinary** .  
  
        > [!NOTE]  
        >  Estas restrições de modificação de coluna também se aplicam para indexar colunas de chave.  
  
##### <a name="design-recommendations"></a>Recomendações de design  
 Redesenhe índices não clusterizados com um comprimento de chave de índice, de tal forma que apenas as colunas usadas para buscas e pesquisas sejam colunas de chave. Faça todas as outras colunas que abrangem a consulta colunas não chave incluídas. Deste modo, você terá todas as colunas necessárias para abranger a consulta, mas a chave de índice em si é pequena e eficiente.  
  
 Por exemplo, suponha que você quer projetar um índice para abranger a consulta seguinte.  
  
```  
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
```  
  
 Para abranger a consulta, cada coluna deve ser definida no índice. Embora você possa definir todas as colunas como colunas de chave, o tamanho chave seria de 334 bytes. Em razão da única coluna de fato usada como critério de pesquisa ser a coluna `PostalCode` , que tem um comprimento de 30 bytes, um melhor design de índice definiria `PostalCode` como sendo a coluna de chave e incluiria todas as outras colunas como colunas que não são colunas de chave.  
  
 A seguinte declaração cria um índice com colunas incluídas para abranger a consulta.  
  
```  
CREATE INDEX IX_Address_PostalCode  
ON Person.Address (PostalCode)  
INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
```  
  
##### <a name="performance-considerations"></a>Considerações sobre desempenho  
 Evite a adição desnecessária de colunas. Adicionar muitas colunas de índice, sejam elas chave ou não, pode gerar as seguintes implicações no desempenho:  
  
-   Poucas filas de índice se ajustarão em uma página. Isto poderia criar aumentos de E/S e eficiência de cache reduzida.  
  
-   Será necessário mais espaço em disco para armazenar o índice. Em particular, acrescentar os tipos de dados **varchar(max)**, **nvarchar(max)**, **varbinary(max)**ou **xml** como colunas de índice não chave pode aumentar significativamente os requisitos de espaço em disco. Isto porque os valores de coluna são copiados no nível folha de índice. Portanto, eles residem no índice e na tabela base.  
  
-   A manutenção do índice pode aumentar o tempo necessário para executar modificações, inserções, atualizações ou exclusões, para a tabela subjacente ou exibição indexada.  
  
 Você terá que determinar se os ganhos no desempenho de consulta superam o efeito no desempenho durante a modificação de dados, e em requisitos adicionais de espaço em disco.  
  
  
##  <a name="Unique"></a> Diretrizes de design de índice exclusivo  
 Um índice exclusivo garante que a chave de índice não contém nenhum valor duplicado e, portanto, cada linha na tabela é exclusiva de algum modo. Especificar um índice exclusivo só faz sentido quando a exclusividade for uma característica dos próprios dados. Por exemplo, se você quiser garantir que os valores na coluna `NationalIDNumber` na tabela `HumanResources.Employee` sejam exclusivos, quando a chave primária for `EmployeeID`, crie uma restrição UNIQUE na coluna `NationalIDNumber` . Se o usuário tentar digitar o mesmo valor naquela coluna para mais de um empregado, será exibida uma mensagem de erro e o valor duplicado não é inserido.  
  
 Com índices exclusivos de multicolunas, o índice garante que cada combinação de valores na chave de índice é exclusivo. Por exemplo, se um índice exclusivo for criado em uma combinação de colunas `LastName`, `FirstName`e `MiddleName` , duas linhas na tabela não poderão ter a mesma combinação de valores que essas colunas.  
  
 Tanto os índices clusterizados quanto os não clusterizados podem ser exclusivos. Contanto que os dados na coluna sejam exclusivos, você pode criar um índice clusterizado exclusivo e não clusterizado na mesma tabela.  
  
 Os benefícios dos índices exclusivos incluem o seguinte:  
  
-   A integridade de dados das colunas definidas é garantida.  
  
-   São fornecidas informações úteis adicionais ao otimizador de consultas.  
  
 Criar uma restrição PRIMARY KEY ou UNIQUE automaticamente gera um índice exclusivo nas colunas especificadas. Não há nenhuma diferença significativa entre criar uma restrição UNIQUE e criar um índice exclusivo independente de uma restrição. A validação de dados ocorre da mesma maneira e o otimizador de consultas não diferencia entre um índice exclusivo criado por uma restrição ou manualmente. Entretanto, você deverá criar uma restrição UNIQUE ou PRIMARY KEY na coluna quando o objetivo for a integridade de dados. Fazendo isso o objetivo do índice será claro.  
  
### <a name="considerations"></a>Considerações  
  
-   Um índice exclusivo, uma restrição UNIQUE ou uma restrição PRIMARY KEY não poderão ser criados, se existirem valores de chave duplicados nos dados.  
  
-   Se os dados forem exclusivos e você quiser impor exclusividade, criar um índice exclusivo em vez de um índice não exclusivo, na mesma combinação de colunas, fornecerá informações adicionais para otimizador de consultas que poderá produzir planos de execução mais eficientes. Criar um índice exclusivo (preferivelmente criando uma restrição UNIQUE) é recomendável nesse caso.  
  
-   Um índice não clusterizado exclusivo pode conter colunas não chave incluídas. Para obter mais informações, consulte [Índice com colunas incluídas](#Included_Columns).  
  
  
##  <a name="Filtered"></a> Diretrizes de criação de índice filtrado  
 Um índice filtrado é um índice não clusterizado otimizado, criado especialmente para consultas que fazem seleções a partir de um subconjunto bem-definido de dados. Ele usa um predicado de filtro para indexar uma parte das linhas da tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta e reduzir os custos de manutenção e armazenamento do índice em comparação com os índices de tabela completa.  
  
||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|  
  
 Os índices filtrados podem oferecer as seguintes vantagens com relação aos índices de tabela completa:  
  
-   **Melhor desempenho de consultas e qualidade de plano**  
  
     Um índice filtrado bem projetado melhora o desempenho das consultas e a qualidade do plano de execução porque é menor do que um índice não clusterizado de tabela completa e possui estatísticas filtradas. As estatísticas filtradas são mais precisas do que as estatísticas de tabela completa, pois abrangem apenas as linhas do índice filtrado.  
  
-   **Redução dos custos de manutenção do índice**  
  
     A manutenção do índice é feita apenas quando as instruções DML (linguagem de manipulação de dados) afetam os dados do índice. Um índice filtrado reduz os custos de manutenção em comparação com o índice não clusterizado de tabela completa porque é menor e a manutenção é feita somente quando seus dados são afetados. É possível ter um grande número de índices filtrados, especialmente quando eles contêm dados que são raramente afetados. Do mesmo modo, se um índice filtrado tiver apenas dados afetados com frequência, seu tamanho reduzido diminuirá o custo de atualização das estatísticas.  
  
-   **Redução dos custos de armazenamento do índice**  
  
     A criação de um índice filtrado pode reduzir o armazenamento em disco de índices não clusterizados quando um índice de tabela completa não é necessário. É possível substituir um índice não clusterizado de tabela completa por vários índices filtrados sem aumentar de forma significativa os requisitos de armazenamento.  
  
 Os índices filtrados são úteis quando as colunas contêm subconjuntos de dados bem-definidos, a que as consultas fazem referência em instruções SELECT. São exemplos:  
  
-   Colunas esparsas que contêm apenas alguns valores não NULL.  
  
-   Colunas heterogêneas que contêm categorias de dados.  
  
-   Colunas que contêm intervalos de valores como quantias em dinheiro, hora e datas.  
  
-   Partições de tabela definidas pela lógica de comparação simples para obter valores de coluna.  
  
 O custo de manutenção reduzido dos índices filtrados é mais perceptível quando o número de linhas do índice é pequeno, se comparado a um índice de tabela completa. Se o índice filtrado incluir a maioria das linhas da tabela, sua manutenção poderá ser mais cara do que a do índice de tabela completa. Nesse caso, você deve usar um índice de tabela completa em vez do índice filtrado.  
  
 Os índices filtrados são definidos em uma tabela e oferecem suporte apenas a operadores de comparação simples. Se você precisar de uma expressão de filtro que referencie várias tabelas ou que tenha uma lógica complexa, deverá criar uma exibição.  
  
### <a name="design-considerations"></a>Considerações de criação  
 Para criar índices filtrados eficazes, é importante entender quais consultas o aplicativo usa e como elas se relacionam com os subconjuntos de dados. Alguns exemplos de dados com subconjuntos bem-definidos são as colunas com valores predominantemente NULL, as colunas com categorias de valores heterogêneas e as colunas com intervalos de valores diferentes. As considerações sobre criação a seguir apresentam uma variedade de cenários em que um índice filtrado pode ser vantajoso com relação aos índices de tabela completa.  
  
#### <a name="filtered-indexes-for-subsets-of-data"></a>Índices filtrados para subconjuntos de dados  
 Quando a coluna tem apenas uma pequena quantidade de valores relevantes para consultas, você pode criar um índice filtrado no subconjunto de valores. Por exemplo, se os valores de uma coluna forem predominantemente NULL e a consulta selecionar apenas valores não NULL, será possível criar um índice filtrado para linhas de dados não NULL. O índice resultante será menor e sua manutenção será menos dispendiosa em comparação com um índice não clusterizado de tabela completa definido nas mesmas colunas de chave.  
  
 Por exemplo, o banco de dados `AdventureWorks2012` tem uma tabela `Production.BillOfMaterials` com 2.679 linhas. A coluna `EndDate` tem apenas 199 linhas que contêm um valor não NULL e outras 2.480 linhas que contêm NULL. O índice filtrado a seguir abrange consultas que retornam as colunas definidas no índice e que selecionam apenas linhas com valor não NULL para `EndDate`.  
  
```  
CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL ;  
GO  
```  
  
 O índice filtrado `FIBillOfMaterialsWithEndDate` é válido para a consulta a seguir. Você pode exibir o plano de execução da consulta para determinar se o otimizador de consulta usou o índice filtrado.  
  
```  
SELECT ProductAssemblyID, ComponentID, StartDate   
FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL   
    AND ComponentID = 5   
    AND StartDate > '20080101' ;  
```  
  
 Para obter mais informações sobre como criar índices filtrados e definir a expressão de predicado do índice filtrado, consulte [Create Filtered Indexes](../relational-databases/indexes/create-filtered-indexes.md).  
  
#### <a name="filtered-indexes-for-heterogeneous-data"></a>Índices filtrados para dados heterogêneos  
 Quando a tabela contém linhas de dados heterogêneos, é possível criar um índice filtrado para uma ou mais categorias de dados.  
  
 Por exemplo, a cada produto listado na tabela `Production.Product` é atribuído um `ProductSubcategoryID`que, por sua vez, está associado às categorias de produtos Bikes, Components, Clothing ou Accessories. Essas categorias são heterogêneas porque os valores das coluna da tabela `Production.Product` não estão estreitamente correlacionados. Por exemplo, as colunas `Color`, `ReorderPoint`, `ListPrice`, `Weight`, `Class`e `Style` têm características exclusivas para cada categoria de produto. Suponha que haja consultas frequentes sobre acessórios que possuem subcategorias entre 27 e 36. É possível aprimorar o desempenho das consultas sobre acessórios criando um índice filtrado nas subcategorias de acessórios, conforme ilustrado no exemplo a seguir.  
  
```  
CREATE NONCLUSTERED INDEX FIProductAccessories  
    ON Production.Product (ProductSubcategoryID, ListPrice)   
        Include (Name)  
WHERE ProductSubcategoryID >= 27 AND ProductSubcategoryID <= 36;  
  
```  
  
 O índice filtrado `FIProductAccessories` abrange a seguinte consulta porque os resultados da consulta  
  
 estão contidos no índice e o plano da consulta não inclui uma pesquisa de tabela base. Por exemplo, a expressão de predicado da consulta `ProductSubcategoryID = 33` é um subconjunto do predicado de índice filtrado `ProductSubcategoryID >= 27` e `ProductSubcategoryID <= 36`, as colunas `ProductSubcategoryID` e `ListPrice` no predicado de consulta são ambas colunas de chave no índice, e o nome é armazenado no nível folha do índice como uma coluna incluída.  
  
```  
SELECT Name, ProductSubcategoryID, ListPrice  
FROM Production.Product  
WHERE ProductSubcategoryID = 33 AND ListPrice > 25.00 ;  
  
```  
  
#### <a name="key-columns"></a>Colunas de Chave  
 Uma prática recomendada é incluir um pequeno número de colunas de chave ou incluídas em uma definição de índice filtrado e inserir apenas as colunas necessárias para o otimizador de consulta escolher o índice filtrado para o plano de execução da consulta. O otimizador de consulta pode escolher um índice filtrado para a consulta, independentemente de ele abranger ou não a consulta. No entanto, é mais provável que o otimizador de consulta escolha um índice filtrado se ele abranger a consulta.  
  
 Em alguns casos, um índice filtrado abrange a consulta sem incluir as colunas na expressão do índice filtrado como colunas de chave ou incluídas na definição do índice filtrado. As diretrizes a seguir explicam quando uma coluna em uma expressão de índice filtrado deve ser uma coluna de chave ou incluída na definição do índice filtrado. Os exemplos se referem ao índice filtrado `FIBillOfMaterialsWithEndDate` que foi criado anteriormente.  
  
 A coluna na expressão do índice filtrado não precisará ser uma coluna de chave ou incluída na definição do índice filtrado, se a expressão do índice filtrado for equivalente ao predicado da consulta e a consulta não retorná-la com os resultados da consulta. Por exemplo, `FIBillOfMaterialsWithEndDate` abrange a consulta a seguir porque o predicado da consulta é equivalente à expressão de filtro e `EndDate` não é retornado com os resultados da consulta. `FIBillOfMaterialsWithEndDate` não precisa de `EndDate` como uma coluna de chave ou incluída na definição do índice filtrado.  
  
```  
SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL;   
```  
  
 A coluna na expressão de índice filtrado deverá ser uma coluna de chave ou incluída na definição do índice filtrado se o predicado de consulta usá-la em uma comparação que não for equivalente à expressão do índice filtrado. Por exemplo, `FIBillOfMaterialsWithEndDate` é válido para a consulta a seguir, porque seleciona um subconjunto de linhas do índice filtrado. Contudo, não abrange a consulta a seguir porque `EndDate` é usado na comparação de `EndDate > '20040101'`, que não é equivalente à expressão do índice filtrado. O processador de consultas não pode executar essa consulta sem observar os valores de `EndDate`. Portanto, `EndDate` deve ser uma coluna de chave ou incluída na definição do índice filtrado.  
  
```  
SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
WHERE EndDate > '20040101';   
```  
  
 A coluna na expressão do índice filtrado deverá ser uma coluna de chave ou incluída na definição do índice filtrado se fizer parte do conjunto de resultados da consulta. Por exemplo, `FIBillOfMaterialsWithEndDate` não abrange a consulta a seguir, porque retorna a coluna `EndDate` nos resultados da consulta. Portanto, `EndDate` deve ser uma coluna de chave ou incluída na definição do índice filtrado.  
  
```  
SELECT ComponentID, StartDate, EndDate FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL;  
```  
  
 A chave de índice clusterizado da tabela não precisa ser uma coluna de chave ou incluída na definição do índice filtrado. A chave de índice clusterizado é incluída automaticamente em todos os índices não clusterizados, inclusive índices filtrados.  
  
#### <a name="data-conversion-operators-in-the-filter-predicate"></a>Operadores de conversão de dados no predicado do filtro  
 Se o operador de comparação especificado na expressão do índice filtrado resultar em uma conversão de dados implícita ou explícita, ocorrerá um erro se a conversão ocorrer à esquerda do operador de comparação. Uma solução seria gravar a expressão do índice filtrado com o operador de conversão de dados (CAST ou CONVERT) à direita do operador de comparação.  
  
 O exemplo a seguir cria uma tabela com diversos tipos de dados.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.TestTable (a int, b varbinary(4));  
  
```  
  
 Na definição de índice filtrado a seguir, a coluna `b` é convertida implicitamente em um tipo de dados de número inteiro para comparação com a constante 1. Isso gera a mensagem de erro 10611 porque a conversão ocorre à esquerda do operador no predicado filtrado.  
  
```  
CREATE NONCLUSTERED INDEX TestTabIndex ON dbo.TestTable(a,b)  
WHERE b = 1;  
```  
  
 A solução é converter a constante à direita para o mesmo tipo da coluna `b`, como mostra o seguinte exemplo:  
  
```  
CREATE INDEX TestTabIndex ON dbo.TestTable(a,b)  
WHERE b = CONVERT(Varbinary(4), 1);  
```  
  
 A movimentação da conversão de dados da esquerda para a direita de um operador de comparação pode alterar o significado da conversão. No exemplo anterior, quando o operador CONVERT foi adicionado à direita, a comparação mudou de uma comparação de número inteiro para uma comparação **varbinary** .  
  
  
##  <a name="Additional_Reading"></a> Leitura adicional  
[Melhorando o desempenho com exibições indexadas do SQL Server 2008](http://msdn.microsoft.com/library/dd171921(v=sql.100).aspx)  
[Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  

