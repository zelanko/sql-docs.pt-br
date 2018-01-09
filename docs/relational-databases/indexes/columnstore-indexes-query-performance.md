---
title: "Índices columnstore – desempenho de consultas | Microsoft Docs"
ms.custom: 
ms.date: 12/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83acbcc4-c51e-439e-ac48-6d4048eba189
caps.latest.revision: "23"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 97c0483870e4f99b68265a09337109f1f0ce0ac2
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="columnstore-indexes---query-performance"></a>Índices columnstore – desempenho de consultas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Recomendações para atingir desempenho de consultas muito rápido, que os índices columnstore são projetados para fornecer.    
    
 Índices ColumnStore podem atingir desempenho até 100 vezes melhor em análise e data warehousing de cargas de trabalho e até 10 vezes melhor compactação de dados que os índices rowstore tradicionais. Essas recomendações ajudam a atingir um desempenho de consultas muito rápido nas consultas que os índices columnstore foram projetados para fornecer. No final, há mais explicações sobre desempenho com columnstore.    
    
## <a name="recommendations-for-improving-query-performance"></a>Recomendações para melhorar o desempenho de consultas    
 Veja a seguir algumas recomendações para atingir o alto desempenho que os índices columnstore foram projetados para fornecer.    
    
### <a name="1-organize-data-to-eliminate-more-rowgroups-from-a-full-table-scan"></a>1. Organizar dados para eliminar mais rowgroups de uma verificação de tabela completa    
    
-   **Aproveite a ordem de inserção.** Geralmente, no data warehouse tradicional, os dados são realmente inseridos na ordem de tempo e a análise é feita na dimensão temporal. Por exemplo, ao analisar vendas por trimestre. Para essa variante de carga de trabalho, a eliminação de rowgroup ocorre automaticamente. No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode descobrir que rowgroups de número foram ignorados como parte do processamento de consulta.    
    
-   **Aproveite o índice rowstore clusterizado.** Se o predicado de consulta comum estiver em uma coluna (por exemplo, C1) que não está relacionada à ordem de inserção da linha, você poderá criar um índice clusterizado rowstore em colunas C1 e, em seguida, criar o índice columstore clusterizado com a remoção do índice rowstore clusterizado. Se você criar o índice columnstore clusterizado explicitamente usando `MAXDOP = 1`, o índice columnstore clusterizado resultante estará ordenado perfeitamente na coluna C1. Se você especificar `MAXDOP = 8`, verá a sobreposição de valores em oito rowgroups. Um caso comum dessa estratégia é quando você cria inicialmente o índice columnstore com um grande conjunto de dados. Observe que, para o NCCI (índice columnstore não clusterizado), se a tabela rowstore base tiver um índice clusterizado, as linhas já estarão ordenadas. Nesse caso, o índice columnstore não clusterizado resultante será ordenado automaticamente. Um ponto importante a observar é que o índice columnstore não mantém a ordem das linhas inerentemente. Conforme novas linhas são inseridas ou linhas mais antigas são atualizadas, talvez seja necessário repetir o processo, já que o desempenho de consultas de análise pode se deteriorar    
    
-   **Aproveite o particionamento de tabela.** Você pode particionar o índice columnstore e, em seguida, usar a eliminação de partição para reduzir o número de rowgroups a serem examinados. Por exemplo, uma tabela de fatos armazena as compras feitas por clientes e um padrão de consulta comum é encontrar as compras trimestrais feitas por um cliente específico; você pode combinar a ordem de inserção com o particionamento na coluna de clientes. Cada partição conterá linhas na ordem de tempo para o cliente específico.    
    
### <a name="2-plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>2. Planejar memória suficiente para criar índices columnstore em paralelo    
 Criar um índice columnstore é, por padrão, uma operação paralela, a menos que a memória seja restrita. Criar o índice em paralelo exige mais memória do que criar o índice em série. Quando há bastante memória, a criação de um índice columnstore assume a ordem de 1,5 vezes mais longa do que a criação de uma árvore B nas mesmas colunas.    
    
 A memória necessária para criar um índice columnstore depende do número de colunas, do número de colunas de cadeia de caracteres, do grau de paralelismo (DOP) e as características dos dados. Por exemplo, se a tabela tiver menos de um milhão de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará apenas um thread para criar o índice columnstore.    
    
 Se a tabela tiver mais de um milhão de linhas, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não puder obter uma concessão de memória suficiente para criar o índice usando MAXDOP, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diminuirá automaticamente `MAXDOP`, conforme necessário, de acordo com a concessão de memória disponível.  Em alguns casos, o DOP deve ser diminuído para um para criar o índice na memória restrita.    
    
 A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a consulta operará sempre no modo de lote. Em versões anteriores, a execução em lotes só é usada quando o DOP é maior do que um.    
    
## <a name="columnstore-performance-explained"></a>Desempenho ColumnStore explicado    
 Índices columnstore atingem alto desempenho de consultas combinando o processamento no modo de lotes in-memory em alta velocidade com técnicas que reduzem consideravelmente os requisitos de E/S.  Já que consultas de análise examinam grandes números de linhas, elas são normalmente associadas a E/S e, portanto, a redução da E/S durante a execução da consulta é crítica para o design de índices columnstore.  Depois que os dados são lidos na memória, é essencial reduzir o número de operações in-memory.    
    
 Índices columnstore reduzem a E/S e otimizam as operações in-memory por meio de alta compactação de dados, eliminação de columnstores, eliminação de rowgroups e processamento em lotes.    
    
### <a name="data-compression"></a>Compactação de dados    
 Índices columnstore obtêm compactação de dados até 10x maior que índices rowstore. Isso reduz significativamente a E/S necessária para executar consultas de análise e, portanto, melhora o desempenho de consultas.    
    
-   Índices columnstore leem dados compactados do disco, o que significa que menos bytes de dados precisam ser lidos da memória.    
    
-   Índices columnstore armazenam dados em formato compactado na memória, o que reduz a E/S com a redução do número de vezes que os mesmos dados são lidos na memória. Por exemplo, com uma compactação de 10 vezes, os índices columnstore podem manter 10 vezes mais dados na memória do que é possível armazenando os dados em formato descompactado. Com mais dados na memória, é mais provável que o índice columnstore localize os dados de que precisa na memória com a realização de leituras de disco adicionais.    
    
-   Os índices columnstore compactam dados por colunas em vez de compactá-los por linhas, o que alcança altas taxas de compactação e reduz o tamanho dos dados armazenados no disco. Cada coluna é compactada e armazenada de modo independente.  Dados em uma coluna sempre têm o mesmo tipo de dados e tendem a ter valores semelhantes. Técnicas de compactação de dados são muito boas para alcançar taxas mais altas de compactação quando os valores são semelhantes.    
    
-   Por exemplo, se uma tabela de fatos armazena endereços de clientes e tem uma coluna de país, o número total de valores possíveis é inferior a 200. Alguns desses valores serão repetidas várias vezes. Se a tabela de fatos tem 100 milhões de linhas, a coluna de país será compactada facilmente e exigirá muito pouco armazenamento. A compactação de linha por linha não é capaz de aproveitar a similaridade de valores de coluna dessa maneira e usará mais bytes para compactar os valores na coluna de país.    
    
### <a name="column-elimination"></a>Eliminação de colunas    
 Índices columnstore ignoram a leitura em colunas que não são necessárias para o resultado da consulta. Essa capacidade, chamada de eliminação de colunas, reduz ainda mais a E/S para a execução de consultas e, portanto, melhora o desempenho delas.    
    
-   A eliminação de colunas é possível porque os dados são organizados e compactados coluna por coluna. Por outro lado, quando os dados são armazenados linha por linha, os valores de coluna em cada linha são fisicamente armazenados juntos e não podem ser facilmente separados. O processador de consultas precisa ler em uma linha inteira para recuperar valores de coluna específicos, o que aumenta a E/S porque dados extras são lidos desnecessariamente na memória.    
    
-   Por exemplo, se uma tabela tiver 50 colunas e a consulta utilizar apenas 5 dessas colunas, o índice columnstore buscará apenas 5 colunas do disco. Ela ignora a leitura nas outras 45 colunas. Isso reduz a E/S em outros 90%, supondo que todas as colunas sejam de tamanho similar. Se os mesmos dados forem armazenados em um rowstore, o processador de consulta precisará ler as 45 colunas adicionais.    
    
### <a name="rowgroup-elimination"></a>Eliminação de rowgroups    
 Para verificações de tabela completa, um grande percentual dos dados geralmente não corresponde aos critérios de predicado de consulta. Usando metadados, o índice columnstore pode ignorar a leitura nos rowgroups que não contêm dados necessários para o resultado da consulta, tudo isso sem a E/S real. Essa capacidade, chamada de eliminação de rowgroups, reduz ainda mais a E/S para verificações de tabela completas e, portanto, melhora o desempenho de consultas.    
    
 **Quando um índice columnstore precisa executar uma verificação de tabela completa?**    
    
 A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], é possível criar um ou mais índices de árvore B regulares não clusterizados em um índice columnstore clusterizado, assim como é possível fazer no heap de um rowstore. Os índices de árvore B não clusterizados podem acelerar uma consulta que contém um predicado de igualdade ou um predicado com um intervalo de valores pequeno.  Para predicados mais complicados, o otimizador de consulta pode escolher uma verificação de tabela completa. Sem a capacidade de ignorar rowgroups, uma verificação de tabela completa seria muito demorada, especialmente para tabelas grandes.    
    
 **Quando uma consulta de análise se beneficia de eliminação de rowgroups para uma verificação de tabela completa?**    
    
 Por exemplo, uma empresa de varejo modelou seus dados de vendas usando uma tabela de fatos com um índice columnstore clusterizado. Cada nova venda armazena vários atributos da transação, incluindo a data da venda de um produto. Curiosamente, mesmo que os índices columnstore não garantam uma ordem de classificação, as linhas nessa tabela serão carregadas em uma ordem classificada por data. Ao longo do tempo, essa tabela aumentará. Embora o negócio varejista possa manter dados de vendas pelos últimos 10 anos, uma consulta de análise talvez precise apenas computar uma agregação do último trimestre. Índices columnstore podem eliminar o acesso aos dados dos 39 trimestres anteriores, apenas observando os metadados da coluna de data. Isso é uma redução de 97% adicionais na quantidade de dados lidos na memória e processados.    
    
 **Quais rowgroups são ignorados em uma verificação de tabela completa?**    
    
 Para determinar quais grupos de linhas eliminar, o índice columnstore usa metadados para armazenar os valores mínimo e máximo de cada segmento de coluna para cada rowgroup. Quando nenhum dos intervalos de segmento de coluna atendem aos critérios de predicado de consulta, o rowgroup inteiro é ignorado sem fazer nenhuma E/S real. Isso funciona porque os dados geralmente são carregados em uma ordem classificada e, embora não exista garantia de que as linhas são classificadas, valores de dados semelhantes geralmente estão localizados no mesmo rowgroup ou em outro adjacente.    
    
 Para obter mais detalhes sobre rowgroups, consulte Guia de índices Columnstore    
    
### <a name="batch-mode-execution"></a>Execução em modo de lote    
 A execução em modo de lote refere-se ao processamento de um conjunto de linhas, normalmente até 900, agrupadas para eficiência de execução. Por exemplo, a consulta `SELECT SUM (Sales) FROM SalesData` agrega as vendas totais da tabela SalesData. Na execução em modo de lote, o mecanismo de execução de consulta calcula a agregação de 900 valores em grupo. Isso estende aos metadados os custos de acesso e outros tipos de sobrecarga em todas as linhas em um lote, em vez de pagar o custo para cada linha; assim, o caminho do código é reduzido significativamente. Processamento de modo de lote opera nos dados compactados quando possível e elimina alguns dos operadores de troca usados pelo processamento de modo de linha. Isso acelera a execução de consultas de análise em ordens de magnitude.    
    
 Nem todos os operadores de execução de consulta podem ser executados em modo de lote. Por exemplo, operações DML como Insert, Delete ou Update são executadas em uma linha por vez. O modo de lote destina-se a operadores voltados à aceleração do desempenho de consultas, como Scan, Join, Aggregate, sort e outros mais. Como o índice columnstore foi introduzido no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], há um esforço contínuo para expandir os operadores que podem ser executados no modo de lote. A tabela abaixo mostra os operadores executados no modo de lote, de acordo com a versão do produto.    
    
|Operadores no modo de lote|Quando isso é usado?|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]¹|Comentários|    
|---------------------------|------------------------|---------------------|---------------------|---------------------------------------|--------------|    
|Operações DML (insert, delete, update, merge)||não|não|não|DML não é uma operação de modo de lote porque ele não é paralelo. Mesmo quando podemos habilitar o processamento em lotes de modo serial, não vemos ganhos significativos ao permitir que o DML seja processado em modo em lote.|    
|verificação de índice columnstore|SCAN|NA|sim|sim|Para índices columnstore, podemos enviar por push o predicado por push para o nó SCAN.|    
|Verificação de índice columnstore (não clusterizado)|SCAN|sim|sim|sim|sim|    
|busca de índice||NA|NA|não|Executamos uma operação de busca por meio de um índice de árvore B não clusterizado no modo de linha.|    
|computar escalar|Uma expressão que é avaliada como um valor escalar.|sim|sim|sim|Há algumas restrições para o tipo de dados. Isso é verdadeiro para todos os operadores de modo de lote.|    
|concatenação|UNION e UNION ALL|não|sim|sim||    
|filtro|Aplicação de predicados|sim|sim|sim||    
|correspondência de hash|Funções de agregação baseadas em hash, junção de hash externa, junção de hash à direita, junção de hash à esquerda, junção interna direita, junção interna esquerda|sim|sim|sim|Restrições de agregação: nenhum mín/máx para cadeias de caracteres. As funções de agregação disponíveis são sum/count/avg/min/max.<br />Restrições de associação: nenhum tipo incompatível ingressa em tipos não inteiros.|    
|junção de mesclagem||não|não|não||    
|consultas multithread||sim|sim|sim||    
|loops aninhados||não|não|não||    
|consultas de thread único executando no MAXDOP 1||não|não|sim||    
|consultas de thread único com um plano de consulta serial||não|não|sim||    
|classificar|Classificar por cláusula em SCAN com índice columnstore.|não|não|sim||    
|classificação superior||não|não|sim||    
|agregações de janela||NA|NA|sim|Novo operador do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|    
    
 ¹Aplica-se ao [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 Premium Edition e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]    
    
### <a name="aggregate-pushdown"></a>Aplicação de agregação    
 Um caminho de execução normal para a computação de agregação para buscar as linhas qualificadas do nó SCAN e agregar os valores no Modo de Lote. Embora isso ofereça bom desempenho, no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a operação de agregação pode ser enviada por push para o nó SCAN para melhorar o desempenho da computação de agregação em ordens de magnitude além da execução do Modo de Lote, desde que as seguintes condições sejam atendidas: 
 
-    As agregações são `MIN`, `MAX`, `SUM`, `COUNT` e `COUNT(*)`. 
-  O operador de agregação deve ficar sobre o nó SCAN ou o nó SCAN com `GROUP BY`.
-  Essa agregação não é uma agregação de distinção.
-  A coluna de agregação não é uma coluna de cadeia de caracteres.
-  A coluna de agregação não é uma coluna virtual. 
-  O tipo de dados de entrada e saída deve ser um dos seguintes e deve ter menos de 64 bits.
    -  `tinyint`, `int`, `bigint`, `smallint`, `bit`
    -  `smallmoney`, `money`, `decimal` e `numeric` com precisão inferior ou igual a 18
    -  `smalldate`, `date`, `datetime`, `datetime2`, `time`
    
 A propagação de agregação é ainda mais acelerada pela agregação eficiente nos dados compactados/codificados em execução amigável a cache e aproveitando SIMD    
    
 ![aggregate pushdown](../../relational-databases/indexes/media/aggregate-pushdown.jpg "aggregate pushdown")    
    
Por exemplo, a aplicação de agregação é feita em ambas as consultas abaixo:    
    
```sql     
SELECT  productkey, SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
GROUP BY productkey    
    
SELECT  SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
```    
    
### <a name="string-predicate-pushdown"></a>Aplicação de predicado de cadeia de caracteres    
Ao criar um esquema de data warehouse, a modelagem de esquema recomendada é usar um esquema estrela ou floco de neve, consistindo em uma ou mais tabelas de fatos e muitas tabelas de dimensões. A [tabela de fatos](https://en.wikipedia.org/wiki/Fact_table) armazena as transações ou medidas de negócios e a [tabela de dimensões](https://en.wikipedia.org/wiki/Dimension_table) armazena as dimensões pelas quais os fatos precisam ser analisados.    
    
Por exemplo, um fato pode ser um registro que representa uma venda de um produto específico em uma região específica, enquanto a dimensão representa um conjunto de regiões, produtos e assim por diante. As tabelas de fatos e dimensões são conectadas por meio de uma relação de chaves primária/estrangeira. As consultas de análise mais comumente usadas unem uma ou mais tabelas de dimensão à tabela de fatos.    
    
Vamos considerar uma tabela de dimensões `Products`. Uma chave primária típica será `ProductCode`, que normalmente é representada como um tipo de dados String. Para o desempenho de consultas, uma melhor prática é criar uma chave alternativa, normalmente uma coluna de inteiros, para referir-se à linha na tabela de dimensões da tabela de fatos.    
    
O índice columnstore executa consultas de análise com junções/predicados que envolvem chaves baseadas em valores numéricos ou inteiros de maneira muito eficiente. No entanto, em muitas cargas de trabalho do cliente, observamos o uso de colunas baseadas em cadeias de caracteres vinculando tabelas de fatos/dimensões e, como resultado, o desempenho de consultas com um índice columnstore não era tão bom. O [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] melhora consideravelmente o desempenho de consultas de análise com colunas baseadas em cadeia de caracteres, ao realizar a aplicação dos predicados com colunas de cadeia de caracteres ao nó SCAN.    
    
A aplicação de predicado de cadeia de caracteres aproveita o dicionário primário/secundário criado para coluna(s) para melhorar o desempenho de consultas. Por exemplo, consideremos o segmento de coluna de cadeia de caracteres dentro de um rowgroup que consiste de 100 valores de cadeia de caracteres distintos. Isso significa que cada valor de cadeia de caracteres distinto é referenciado 10.000 vezes em média, supondo 1 milhão de linhas.    
    
Com a aplicação de predicado de cadeia de caracteres, a execução da consulta calcula o predicado em relação aos valores no dicionário e se ela se qualificar, todas as linhas se referindo ao valor do dicionário são qualificadas automaticamente. Isso melhora o desempenho de duas maneiras:
1.  Apenas as linhas qualificadas são retornadas, reduzindo o número de linhas que precisam fluir para fora do nó SCAN. 
2.  O número de comparações de cadeias de caracteres é significativamente reduzido. Neste exemplo, apenas 100 comparações de cadeias de caracteres são necessárias, em vez de 1 milhão de comparações. Existem algumas limitações, conforme descrito abaixo:    
    -   Nenhuma aplicação de predicado da cadeia de caracteres para rowgroups delta. Não há nenhum dicionário para colunas em rowgroups delta.    
    -   Não há nenhuma aplicação de predicado de cadeia de caracteres se o dicionário excede 64 KB de entradas.    
    -   Não há suporte para expressões avaliadas como NULLs.    
    
## <a name="see-also"></a>Consulte Também    
 [Diretrizes de design dos Índices columnstore](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Diretrizes de Carregamento de Dados de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)     
 [Índices columnstore para Data Warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Desfragmentação de índices columnstore](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)    
 [Arquitetura de índices columnstore](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)     
  
