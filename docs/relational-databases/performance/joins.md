---
title: Joins (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- HASH join
- NESTED LOOPS join
- MERGE join
- ADAPTIVE join
- joins [SQL Server], about joins
- join hints [SQL Server]
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f4b2bd
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1c7f2ff4782923eef9ee4d91fa0a7c69239e298c
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009686"
---
# <a name="joins-sql-server"></a>Joins (SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa operações de classificação, interseção, união e diferença usando classificação de memória e a tecnologia de junção de hash. Usando esse tipo de plano de consulta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte o particionamento vertical de tabela, algumas vezes denominada armazenamento colunar.   

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emprega quatro tipos de operações de junção:    
-   Junções de Loops Aninhados     
-   Junções de mesclagem   
-   Junções de hash   
-   Junções adaptáveis (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])

## <a name="join-fundamentals"></a><a name="fundamentals"></a> Conceitos básicos de junção
Usando junções, é possível recuperar dados de duas ou mais tabelas com base em relações lógicas entre as tabelas. Junções indicam como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deveria usar dados de uma tabela para selecionar as linhas em outra tabela.    

Uma condição de junção define o modo como duas tabelas são relacionadas em uma consulta por:    
-   Especificando a coluna de cada tabela a ser usada para a junção. Uma condição de junção típica especifica uma chave estrangeira de uma tabela e sua chave associada na outra tabela.    
-   Especificando um operador lógico (por exemplo, = ou <>) a ser usado na comparação de valores das colunas.    

Junções internas podem ser especificadas nas cláusulas `FROM` ou `WHERE`. Junções externas podem ser especificadas apenas na cláusula `FROM`. As condições de junção combinam-se com as condições de pesquisa `WHERE` e `HAVING` para controlar as linhas selecionadas das tabelas base referenciadas na cláusula `FROM`.    

Especificar as condições de junção na cláusula `FROM` ajuda a separá-las de qualquer outro critério de pesquisa que possa ser especificado em uma cláusula `WHERE` e é o método recomendado para a especificação de junções. Uma sintaxe de junção de cláusula ISO FROM simplificada é:

```
FROM first_table join_type second_table [ON (join_condition)]
```

*join_type* especifica que tipo de junção é executado: uma junção interna, externa ou cruzada. *join_condition* define o predicado a ser avaliado para cada par de linhas unidas. O exemplo a seguir é de uma especificação de junção de cláusula FROM:

```sql
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
     ON (ProductVendor.BusinessEntityID = Vendor.BusinessEntityID)
```

O exemplo a seguir é uma instrução SELECT simples que usa esta junção:

```sql
SELECT ProductID, Purchasing.Vendor.BusinessEntityID, Name
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
    ON (Purchasing.ProductVendor.BusinessEntityID = Purchasing.Vendor.BusinessEntityID)
WHERE StandardPrice > $10
  AND Name LIKE N'F%'
GO
```

A seleção retorna o produto e as informações de fornecedor para qualquer combinação de partes fornecidas por uma empresa cujo nome começa com a letra F e o preço do produto é maior que $10.   

Quando várias tabelas são referenciadas em uma única consulta, todas as referências de coluna devem ser inequívocas. No exemplo anterior, a tabela ProductVendor e a tabela Vendor têm ambas uma coluna denominada BusinessEntityID. Qualquer nome de coluna que seja duplicado entre duas ou mais tabelas referenciadas na consulta deve ser qualificado com o nome da tabela. Todas as referências às colunas Vendor no exemplo são qualificadas.   

Quando um nome de coluna não está duplicado em duas ou mais tabelas usadas na consulta, a referências a ele não precisam ser qualificadas com o nome da tabela. Isso é mostrado no exemplo anterior. Por vezes a instrução SELECT é difícil de compreender, pois não há nada que indique a tabela que forneceu cada coluna. A legibilidade da consulta será aprimorada se todas as colunas estiverem qualificadas com seus nomes de tabela. A legibilidade é aperfeiçoada se aliases de tabela são usados, principalmente quando os nomes de tabelas precisam ser qualificados com nomes de proprietários e de banco de dados. O exemplo seguinte é o mesmo, exceto que aliases de tabela foram atribuídos e as colunas foram qualificadas com aliases de tabela para aperfeiçoar a legibilidade:

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv 
JOIN Purchasing.Vendor AS v
    ON (pv.BusinessEntityID = v.BusinessEntityID)
WHERE StandardPrice > $10
    AND Name LIKE N'F%';
```

Os exemplos anteriores especificaram as condições de junção na cláusula FROM, que é o método preferencial. A seguinte consulta contém a mesma condição de junção especificada na cláusula WHERE:

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv, Purchasing.Vendor AS v
WHERE pv.BusinessEntityID=v.BusinessEntityID
    AND StandardPrice > $10
    AND Name LIKE N'F%';
```

A lista de seleção para uma junção pode fazer referência a todas as colunas nas tabelas unidas ou a qualquer subconjunto de colunas. A lista de seleção não precisa conter colunas de todas as tabelas na junção. Por exemplo, em uma junção de três tabelas, somente uma tabela pode ser usada para ligar uma das tabelas à terceira e, nenhuma das colunas da tabela do meio, precisa ser referenciada na lista de seleção.   

Embora as condições de junção tenham comparações de igualdade (=), outros operadores relacionais ou de comparação podem ser especificados, como também outros predicados. Para obter mais informações, veja [Operadores de comparação &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) e [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  

Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processa junções, o mecanismo de consulta escolhe o método mais eficaz (entre várias possibilidades) de processamento da junção. A execução física de várias junções pode usar muitas otimizações diferentes e portanto não pode ser prevista de maneira confiável.   

Colunas usadas em uma condição de junção não precisam ter o mesmo nome ou ter o mesmo tipo de dados. Entretanto, se os tipos de dados não forem idênticos, eles deverão ser compatíveis, ou do tipo que o SQL Server possa converter implicitamente. Se o tipo de dados não puder ser convertido implicitamente, a condição de junção deverá converter explicitamente o tipo de dados usando a função `CAST`. Para obter mais informações sobre conversões implícitas e explícitas, veja [Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).    

A maioria das consultas que usam uma junção pode ser regravada usando uma subconsulta (uma consulta aninhada dentro de outra consulta) e a maioria das subconsultas pode ser regravada como junções. Para obter mais informações sobre subconsultas, veja [Subconsultas](../../relational-databases/performance/subqueries.md).   

> [!NOTE]
> Tabelas não podem ser unidas diretamente em colunas ntext, text ou image. No entanto, as tabelas podem ser unidas indiretamente em colunas ntext, text ou image usando `SUBSTRING`.    
> Por exemplo, `SELECT * FROM t1 JOIN t2 ON SUBSTRING(t1.textcolumn, 1, 20) = SUBSTRING(t2.textcolumn, 1, 20)` executa uma junção interna de duas tabelas nos primeiros 20 caracteres de cada coluna de texto em tabelas t1 e t2.   
> Além disso, outra possibilidade de comparação das colunas ntext ou text de duas tabelas é comparar o comprimento das colunas com a cláusula `WHERE`, por exemplo: `WHERE DATALENGTH(p1.pr_info) = DATALENGTH(p2.pr_info)`

## <a name="understanding-nested-loops-joins"></a><a name="nested_loops"></a> Compreendendo junções de Loops Aninhados
Se uma entrada de junção for pequena (menos que 10 linhas) e a outra entrada de junção for bastante grande e indexada a suas colunas de junção, uma junção de loops aninhados de índice será a operação de junção mais rápida porque eles requerem o mínimo de E/S e comparações. 

A junção de loops aninhados, também denominada *iteração aninhada*, usa uma entrada de junção como a tabela de entrada externa (mostrada como a entrada superior no plano de execução) e outra como a tabela de entrada interna (na parte inferior). O loop externo consome a tabela de entrada externa linha por linha. O loop interno, executado para cada linha externa, pesquisa linhas correspondentes na tabela de entrada interna.   

No caso mais simples, a pesquisa examina toda uma tabela ou índice; isto é chamado de *junção de loops aninhados naive*. Se a pesquisa explorar um índice, será chamado de *junção de loops aninhados de índice*. Se o índice for criado como parte do plano de consulta (e destruído na conclusão da consulta), será chamado de *junção de loops aninhados de índice temporário*. Todas essas variantes são consideradas pelo Otimizador de Consulta.   

Uma junção de loops aninhados será particularmente eficaz se a entrada externa for pequena e a entrada interna for pré-indexada e grande. Em muitas transações pequenas, como as que afetam apenas um pequeno conjunto de linhas, as junções de loops aninhados de índice são superiores às junções mescladas e junções de hash. Em consultas grandes, contudo, as junções de loops aninhados não são frequentemente a melhor escolha.    

Quando o atributo OPTIMIZED de um Operador de junção de loops aninhados é definido como **True**, isso significa que um Loop aninhado otimizado (ou Classificação em lote) é usado para minimizar a E/S quando a tabela de lado interno é grande, independentemente de ser paralelizada ou não. A presença dessa otimização em um determinado plano pode não ser muito óbvia durante a análise de um plano de execução, uma vez que a própria classificação é uma operação oculta. Mas ao examinar o XML do plano para o atributo OPTIMIZED, isso indica que a Junção de loops aninhados pode tentar reordenar as linhas de entrada para melhorar o desempenho de E/S.

## <a name="understanding-merge-joins"></a><a name="merge"></a> Compreendendo Junções de Mesclagem
Se as duas entradas de junção não são pequenas, mas são classificadas na coluna de junção (por exemplo, se foram obtidas de exames em índices classificados), uma junção de mesclagem será a operação de junção mais rápida. Se ambas as entradas de junção forem grandes e as duas entradas forem de tamanhos semelhantes, uma junção de mesclagem com classificação prévia e uma junção de hash oferecerão desempenho semelhante. Porém, operações de junção de hash são muitas vezes mais rápidas quando os dois tamanhos da entrada diferem significativamente um do outro.       

A junção de mescla exige que as duas entradas sejam classificadas nas colunas de mesclagem, que são definidas pelas cláusulas de igualdade (ON) do predicado de junção. O otimizador de consulta geralmente examina um índice, caso exista um no conjunto de colunas, ou coloca um operador de classificação abaixo da junção de mescla. Em casos raros, podem existir diversas cláusulas de igualdade, mas as colunas de mesclagem são tiradas somente de algumas das cláusulas de igualdade disponíveis.    

Uma vez que cada entrada é classificada, o operador **Junção de Mesclagem** adquire uma linha de cada entrada e as compara. Por exemplo, em operações de junção internas, serão retornadas as linhas que forem iguais. Se elas não forem iguais, será descartada a linha com o menor valor e será obtida outra linha daquela entrada. Esse processo repete-se até que todas as linhas tenham sido processadas.    

A operação mesclar junção pode ser uma operação habitual ou uma operação muitos para muitos. Uma junção de mescla muitos para muitos usa uma tabela temporária para armazenar linhas. Se houver valores duplicados de cada entrada, uma das entradas terá que retroceder ao início das linhas duplicadas à medida que cada linha duplicada da outra entrada for processada.    

Se houver um predicado residual presente, todas as linhas que satisfaçam ao predicado de mesclagem avaliarão o predicado residual e serão retornadas somente as linhas que o satisfaçam.   

A junção de mescla é muito rápida, mas pode ser uma escolha cara se forem necessárias operações de classificação. Porém, se o volume de dados for grande e os dados desejados puderem ser obtidos pré-classificados de índices da árvore B existentes, frequentemente a junção de mescla será o algoritmo de junção mais rápido disponível.    

## <a name="understanding-hash-joins"></a><a name="hash"></a> Compreendendo junções hash
Junções de hash podem processar com eficácia grande volume de entradas não classificadas e não indexadas. Elas são úteis para resultados intermediários em consultas complexas por que:
-   Os resultados intermediários não são indexados (a menos que salvos explicitamente no disco e depois indexados) e muitas vezes não são classificados adequadamente para a próxima operação no plano de consulta.
-   Otimizadores de consulta só calculam tamanhos de resultado intermediário. Como as estimativas podem ser muito imprecisas para consultas complexas, os algoritmos para processar resultados intermediários não só devem ser eficientes, mas também devem ser degradados de forma suave se um resultado intermediário for muito maior do que o previsto.   

A junção de hash permite reduções no uso da desnormalização. A desnormalização é usada geralmente para obter melhor desempenho e reduzir as operações de junção, apesar dos perigos de redundância, como atualizações inconsistentes. As junções de hash reduzem a necessidade a desnormalização. As junções de hash permitem particionamento vertical (representando grupos de colunas de uma única tabela em arquivos separados ou índices) para se tornar uma opção viável no design do banco de dados físico.     

A junção hash tem duas entradas: a entrada **build** e entrada **probe**. O otimizador de consulta nomeia estes papéis de forma que a menor das duas entradas é a entrada de construção.    

Junções de hash são usadas para muitos tipos de operações para definir correspondente: junção interna; esquerda, direita e junção externa completa; semijunção esquerda e direita ; interseção; união; e diferença. Além disso, uma variante da junção de hash pode fazer remoção e agrupamento duplicados, como `SUM(salary) GROUP BY department`. Essas modificações usam só uma entrada para os papéis de construção e investigação.   

As seções seguintes descrevem tipos diferentes de junções de hash: junção de hash em-memória, junção de hash de cortesia e junção de hash recursiva.    

### <a name="in-memory-hash-join"></a><a name="inmem_hash"></a> Junção hash em memória
A junção de hash primeiro verifica ou calcula a entrada de construção inteira e então constrói uma tabela de hash em memória. Cada linha é inserida em um compartimento de memória hash que depende do valor de hash computado para a chave hash. Se a entrada de construção inteira for menor que a memória disponível, todas as linhas poderão ser inseridas na tabela de hash. Essa fase de construção é seguida pela fase de investigação. A entrada de investigação inteira é verificada ou calculada uma linha de cada vez e o valor da chave de hash é calculado para cada linha de investigação, o compartimento de hash correspondente é verificado e as correspondências são produzidas.    

### <a name="grace-hash-join"></a><a name="grace_hash"></a> Junção hash de cortesia
Se a entrada de construção não couber na memória, uma junção de hash continua em vários passos. Isso é conhecido como uma junção hash de cortesia. Cada passo tem uma fase de construção e fase de investigação. Inicialmente, a construção inteira e entradas de investigação são consumidas e particionadas (usando uma função de hash na chave hash) em arquivos múltiplos. Usando a função de hash nas chaves de hash garante que quaisquer dois registros de junção devem estar no mesmo par de arquivos. Portanto, a tarefa de unir duas entradas grandes foi reduzida a instâncias múltiplas, mas menores, das mesmas tarefas. A junção de hash é se aplicada então a cada par de arquivos particionados.    

### <a name="recursive-hash-join"></a><a name="recursive_hash"></a> Junção hash recursiva
Se a entrada de construção for tão grande que entradas para uma fusão externa padrão requereriam níveis de fusão múltiplos, serão requeridos passos de particionamentos múltiplos e níveis de particionamentos múltiplos. Se somente algumas das partições forem grandes, passos de particionamentos adicionais serão usados apenas para essas partições específicas. Para fazer todos os passos de particionamento tão rápido quanto possível, operações grandes, assíncronas de I/O são usadas de forma que um único thread pode manter unidades de disco múltiplas ocupadas.    

> [!NOTE]
> Se a entrada de construção só for ligeiramente maior que a memória disponível, elementos de junção de hash em-memória e junção de hash de cortesia serão combinados em um único passo, produzindo uma junção de hash híbrida.   

Nem sempre  é possível durante otimização determinar qual junção de hash é usada. Portanto, o SQL Server começa usando uma junção hash em memória e gradualmente passa para a junção hash de cortesia e para a junção hash recursiva, dependendo do tamanho da entrada de compilação.    

Se o Otimizador de Consulta prever incorretamente qual das duas entradas será menor e, portanto, deveria ter sido a entrada de compilação, os papéis de compilação e investigação serão invertidos dinamicamente. A junção de hash garante que usa o menor arquivo com excedente como entrada de construção. Essa técnica é chamada de reversão de papel. A reversão de papel acontece dentro da junção de hash depois de pelo menos um derramamento para o disco.     

> [!NOTE]
> A reversão de papel acontece independente de qualquer dica de consulta ou estrutura. A reversão de papel não aparecerá em seu plano de consulta; quando acontecer, é transparente ao usuário.

### <a name="hash-bailout"></a><a name="hash_bailout"></a> Esgotamento de hash
O termo de esgotamento de hash às vezes é usado para descrever junções hash de cortesia ou junções hash recursivas.    

> [!NOTE]
> Junções de hash recursivas ou abandonos de hash causam desempenho reduzido em seu servidor. Se você vir muitos eventos de Aviso de Hash em um rastreamento, atualize as estatísticas nas colunas que estão sendo unidas.    

Para obter mais informações sobre esgotamento de hash, veja [Classe de evento de aviso de Hash](../../relational-databases/event-classes/hash-warning-event-class.md).    

## <a name="understanding-adaptive-joins"></a><a name="adaptive"></a> Como são as junções adaptáveis
As Junções adaptáveis de [Modo de lote](../../relational-databases/query-processing-architecture-guide.md#batch-mode-execution) permitem a escolha de um método de [Junção Hash](#hash) ou de [Junção de loops aninhados](#nested_loops) a ser adiado até **depois** que a primeira entrada for verificada. O operador de Junção Adaptável define um limite que é usado para decidir quando mudar para um plano de Loops aninhados. Portanto, um plano de consulta pode alternar dinamicamente para uma estratégia de junção melhor durante a execução sem precisar ser recompilado. 

> [!TIP]
> As cargas de trabalho com oscilações frequentes entre verificações de entradas de junção pequenas e grandes terão mais benefícios com esse recurso.

A decisão de runtime se baseia nas seguintes etapas:
-  Se a contagem de linhas da entrada de junção de build for pequena o suficiente para que uma Junção de loops aninhados seja mais ideal do que uma Junção Hash, o plano será alternado para um algoritmo de Loops Aninhados.
-  Se a entrada de junção de build exceder um limite de contagem de linhas específico, o plano não mudará e continuará com uma Junção hash.

A consulta a seguir é usada para ilustrar um exemplo de Junção Adaptável:

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

A consulta retorna 336 linhas. Habilitar as [Estatísticas de consultas dinâmicas](../../relational-databases/performance/live-query-statistics.md) exibe o plano a seguir:

![Resultados da consulta: 336 linhas](../../relational-databases/performance/media/4_AQPStats336Rows.png)

No plano, observe o seguinte:
1. Uma verificação de índice columnstore usada para fornecer linhas para a fase de build da Junção hash.
2. O novo operador de Junção Adaptável. Este operador define um limite que é usado para decidir quando mudar para um plano de Loops Aninhados. Para esse exemplo, o limite é de 78 linhas. Tudo que for &gt;= 78 linhas usará uma Junção hash. Quando estiver abaixo do limite, uma junção de Loops aninhados será usada.
3. Como a consulta retorna 336 linhas, excede o limite. Portanto, a segunda branch representa a fase de investigação de uma operação de Junção de hash padrão. Observe que as Estatísticas de consultas dinâmicas mostram as linhas que passam pelos operadores – nesse caso, "672 de 672".
4. E a última branch é uma Busca de índice clusterizado a ser usada pela junção de Loops aninhados que não teve o limite excedido. Observe que podemos ver "0 de 336" linhas exibidas (o branch não é usado).

Agora compare o plano com a mesma consulta, mas quando o valor de *Quantidade* só tem uma linha na tabela:
 
```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
A consulta retorna uma linha. Habilitar as Estatísticas de consultas dinâmicas exibe o plano a seguir:

![Resultado da consulta: uma linha](../../relational-databases/performance/media/5_AQPStatsOneRow.png)

No plano, observe o seguinte:
- Com uma linha retornada, a Busca de índice clusterizado agora tem linhas que passam por ela.
- E, como a fase de build da Junção Hash não continuou, não há linhas passando pela segunda branch.

### <a name="adaptive-join-remarks"></a>Comentários de junção adaptável
As junções adaptáveis apresentam um requisito de memória maior do que um plano equivalente de Junção de Loops Aninhados indexados. A memória adicional é solicitada como se os Loops Aninhados fossem uma Junção hash. Também há sobrecarga para a fase de build como uma operação de “parar e ir” em vez de uma junção equivalente de fluxo de Loops Aninhados. Com esse custo adicional vem a flexibilidade para cenários em que as contagens de linhas podem flutuar na entrada de build.

As Junções adaptáveis de modo de lote funcionam para a execução inicial de uma instrução. Depois que são compiladas, as próximas execuções permanecem adaptáveis com base no limite de Junção Adaptável compilada e nas linhas de runtime que passam pela fase de build da entrada externa.

Se uma Junção Adaptável alterna para uma operação de Loops Aninhados, ela usa as linhas já lidas pelo build de Junção Hash. O operador **não** lê novamente as linhas de referência externa novamente.

### <a name="tracking-adaptive-join-activity"></a>Controlando a atividade da Junção adaptável
O operador de Junção Adaptável tem os seguintes atributos de operador de plano:

|Atributo de plano|DESCRIÇÃO|
|---|---|
|AdaptiveThresholdRows|Mostra o uso de limite para alternar de uma junção hash para uma junção de loops aninhados.|
|EstimatedJoinType|Qual é o provável tipo de junção.|
|ActualJoinType|Em um plano real, mostra qual algoritmo de junção foi finalmente escolhido com base no limite.|

O plano estimado mostra a forma do plano de Junção Adaptável, juntamente com um limite de Junção Adaptável definido e o tipo de junção estimado.

> [!TIP]
> O Repositório de Consultas captura e é capaz de forçar um plano de Junção Adaptável de modo de lote.

### <a name="adaptive-join-eligible-statements"></a>Instruções qualificadas para junção adaptável
Algumas condições tornam uma junção lógica qualificada para uma Junção Adaptável de modo de lote:
- O nível de compatibilidade do banco de dados é 140 ou superior.
- A consulta é uma instrução `SELECT` (as instruções de modificação de dados não são qualificadas no momento).
- A junção é qualificada para ser executada por uma Junção de loops aninhados indexada ou um algoritmo físico de Junção hash.
- A Junção hash usa o [Modo de lote](../../relational-databases/query-processing-architecture-guide.md#batch-mode-execution) – por meio da presença de um Índice columnstore na consulta geral ou de uma Tabela indexada por columnstore referenciada diretamente pela junção.
- As soluções alternativas geradas da Junção de loops aninhados e da Junção hash devem ter o mesmo primeiro filho (referência externa).

### <a name="adaptive-threshold-rows"></a>Linhas de limite adaptável
O gráfico a seguir mostra uma interseção de exemplo entre o custo de uma Junção hash e o custo de uma alternativa de Junção de loops aninhados. Neste ponto de interseção, o limite é determinado e, por sua vez, ele determina o algoritmo real usado para a operação de junção.

![Limite de junção](../../relational-databases/performance/media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>Desabilitar Junções adaptáveis sem alterar o nível de compatibilidade
Junções adaptáveis podem ser desabilitadas no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 140 e superior.  
Para desabilitar as Junções adaptáveis para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

Quando habilitada, essa configuração aparecerá como habilitada em [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md).
Para reabilitar as junções adaptáveis para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = ON;
```

As Junções adaptáveis também podem ser desabilitadas para uma consulta específica designando `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` como uma [dica de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint). Por exemplo:

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
       ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

> [!NOTE]
> Uma dica de consulta USE HINT tem precedência sobre uma configuração de escopo do banco de dados ou uma configuração de sinalizador de rastreamento. 

## <a name="null-values-and-joins"></a><a name="nulls_joins"></a> Valores nulos e junções
Quando há valores nulos nas colunas de tabelas sendo associadas, eles não correspondem uns aos outros. A presença de valores nulos em uma coluna de uma das tabelas que estão sendo associadas pode ser retornada apenas usando uma junção externa (a menos que a cláusula `WHERE` exclua valores nulos).     

Veja duas tabelas que contêm NULL na coluna que participará da junção:     

```
table1                          table2
a           b                   c            d
-------     ------              -------      ------
      1        one                 NULL         two
   NULL      three                    4        four
      4      join4
```    

Uma junção que compara os valores na coluna a com os valores da coluna c não obtém uma correspondência nas colunas que têm valores de NULL:

```sql
SELECT *
FROM table1 t1 JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```  

Somente uma linha com 4 na coluna a e c é retornada:

```
a           b      c           d      
----------- ------ ----------- ------ 
4           join4  4           four   

(1 row(s) affected)
```   

Os valores nulos retornados de uma tabela base também são difíceis de distinguir dos valores nulos retornados de uma junção externa. Por exemplo, a seguinte instrução `SELECT` faz uma junção externa esquerda nestas duas tabelas:   

```sql
SELECT *
FROM table1 t1 LEFT OUTER JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```   

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]   

```
a           b      c           d      
----------- ------ ----------- ------ 
NULL        three  NULL        NULL 
1           one    NULL        NULL 
4           join4  4           four   

(3 row(s) affected)
```   

Os resultados não facilitam a distinção de um NULL nos dados de um NULL que representa uma falha na junção. Quando os valores nulos estão presentes nos dados que estão sendo associados, geralmente é preferível omiti-los nos resultados usando uma junção comum.    

## <a name="see-also"></a>Consulte Também  
[Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[Operadores de comparação &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)    
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
[Subconsultas](../../relational-databases/performance/subqueries.md)      
[Junções adaptáveis](../../relational-databases/performance/intelligent-query-processing.md#batch-mode-adaptive-joins)    
