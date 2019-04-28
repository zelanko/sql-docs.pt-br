---
title: Sintaxe de filtro e exemplos de modelo (Analysis Services - mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- model filter [data mining]
- filter syntax [data mining]
- filters [data mining]
- filters [Analysis Services]
ms.assetid: c729d9b3-8fda-405e-9497-52b2d7493eae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c9c148995dfe83d24798c31900874e4fe3e80df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733137"
---
# <a name="model-filter-syntax-and-examples-analysis-services---data-mining"></a>Sintaxe de filtro de modelo e exemplos (Analysis Services - Mineração de dados)
  Esta seção fornece informações detalhadas sobre a sintaxe de filtros de modelo, além de expressões de exemplo.  
  
 
  
##  <a name="bkmk_Syntax"></a> Filter Syntax  
 As expressões de filtro geralmente são equivalentes ao conteúdo de uma cláusula WHERE. Você pode conectar várias condições usando os operadores lógicos `AND`, `OR` e `NOT`.  
  
 Em tabelas aninhadas, você também pode usar os operadores `EXISTS` e `NOT EXISTS`. Uma condição `EXISTS` será avaliada como `true` se a subconsulta retornar pelo menos uma linha. Isso é útil nos casos em que você deseja restringir o modelo para os casos que contêm um determinado valor na tabela aninhada: por exemplo, os clientes que compraram pelo menos um item uma vez.  
  
 Uma condição `NOT EXISTS` é avaliada como `true` se a condição especificada na subconsulta não existir. Um exemplo é quando você deseja restringir o modelo a clientes que nunca compraram um determinado item.  
  
 A sintaxe geral é:  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *filtro*  
 Contém um ou mais predicados, conectados por operadores lógicos.  
  
 *lista de predicados*  
 Uma ou mais expressões de filtro válidas, separadas por operadores lógicos.  
  
 *columnName*  
 O nome de uma coluna de estrutura de mineração.  
  
 operador lógico  
 `AND`, `OR`, `NOT`  
  
 *avPredicate*  
 Expressão de filtro que pode ser aplicada somente à coluna da estrutura de mineração escalar. Uma expressão *avPredicate* pode ser usada nos filtros de modelo ou filtros de tabelas aninhadas.  
  
 Uma expressão que usa quaisquer dos operadores a seguir só pode ser aplicada a uma coluna contínua. :  
  
-   **\<** (menor que)  
  
-   **>** (maior que)  
  
-   **>=** (maior que ou igual a)  
  
-   **\<=** (menor que ou igual a)  
  
> [!NOTE]  
>  Independentemente do tipo de dados, esses operadores não podem ser aplicados a uma coluna que tenha o tipo `Discrete`, `Discretized` ou `Key`.  
  
 Uma expressão que usa quaisquer dos operadores a seguir só pode ser aplicada a uma coluna contínua, discreta, distinta ou chave:  
  
-   **=** (igual a)  
  
-   **!=** (diferente de)  
  
-   **IS NULL**  
  
 Se o argumento *avPredicate*for aplicado a uma coluna de dados discretos, o valor usado no filtro poderá ser qualquer valor em um bloco específico.  
  
 Em outras palavras, você não define a condição como `AgeDisc = '25-35'`, mas calcula e usa um valor desse intervalo.  
  
 Exemplo:  `AgeDisc = 27`  significa que qualquer valor no mesmo intervalo como 27, que nesse caso é de 25 a 35.  
  
 *nestedTablePredicate*  
 A expressão filtrada aplicada a uma tabela aninhada. Pode ser usado somente nos filtros de modelo.  
  
 O argumento de subconsulta do argumento *nestedTablePredicate*só pode ser aplicada a uma coluna de estrutura de mineração de tabela  
  
 subconsulta  
 Uma instrução SELECT seguida por um predicado válido ou lista de predicados.  
  
 Todos os predicados devem ser do tipo descrito em *avPredicates*. Além disso, os predicados só podem se referir a colunas incluídas na tabela aninhada atual, identificada pelo argumento, *columnName*.  
  
### <a name="limitations-on-filter-syntax"></a>Limitações na sintaxe do filtro  
 As restrições a seguir se aplicam a filtros:  
  
-   Um filtro pode conter somente predicados simples. Esses incluem os operadores matemáticos, escalares e nomes de coluna.  
  
-   Funções definidas pelo usuário não são suportadas na sintaxe de filtro.  
  
-   Operadores não boolianos, como os sinais de mais ou menos, não são suportados na sintaxe de filtro.  
  
## <a name="examples-of-filters"></a>Exemplos de filtros  
 Os exemplos a seguir demonstram o uso de filtros aplicados a um modelo de mineração. Se você criar a expressão de filtro usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na janela **Propriedade** e o painel **Expressão** da caixa de diálogo de filtro, você verá somente a cadeia exibida depois das palavras-chave WITH FILTER. A seguir, a definição da estrutura de mineração incluída para facilitar o entendimento do tipo de coluna e uso.  
  
###  <a name="bkmk_Ex1"></a> Exemplo 1: Filtragem de nível de caso típico  
 Esse exemplo mostra um simples filtro que restringe os casos usados no modelo para clientes cuja ocupação seja arquiteto e cuja idade seja mais de 30 anos.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation='Architect')  
```  
  

  
###  <a name="bkmk_Ex2"></a> Exemplo 2: Filtragem de nível de caso usando atributos da tabela aninhada  
 Se sua estrutura de mineração contiver tabelas aninhadas, você poderá filtrar pela existência de um valor em uma tabela aninhada ou filtrar pelas linhas da tabela aninhada que contêm um valor específico. Esse exemplo restringe os casos usados para o modelo para clientes com mais de 30 anos que fizeram pelo menos uma compra que incluísse leite.  
  
 Como esse exemplo mostra, não é necessário que o filtro use somente colunas incluídas no modelo. A tabela aninhada **Produtos** faz parte da estrutura de mineração, mas não está incluída no modelo de mineração. No entanto, você ainda pode filtrar por valores e atributos na tabela aninhada. Para exibir os detalhes desses casos, o detalhamento deve ser habilitado.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk')  
)  
```  
  
 
  
###  <a name="bkmk_Ex3"></a> Exemplo 3: Filtragem de nível de caso em vários atributos de tabela aninhada  
 Esse exemplo mostra um filtro de três partes: uma condição aplicada à tabela de casos, outra condição para um atributo na tabela aninhada e outra condição em um valor específico em uma das colunas da tabela aninhada.  
  
 A primeira condição no filtro, `Age > 30`, é aplicada a uma coluna na tabela de casos. As outras condições são aplicadas à tabela aninhada.  
  
 A segunda condição, o `EXISTS (SELECT * FROM Products WHERE ProductName='Milk'`verifica a presença de, pelo menos, uma compra na tabela aninhada que inclua leite. A terceira condição, `Quantity>=2`, significa que o cliente deve ter comprado pelo menos duas unidades de leite em uma única transação.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk'  AND Quantity >= 2)   
)  
```  
  

  
###  <a name="bkmk_Ex4"></a> Exemplo 4: Filtragem de nível de caso na ausência de atributos de tabela aninhada  
 Esse exemplo mostra como limitar os casos para o cliente que não comprou um item específico, filtrando pela ausência de um atributo na tabela aninhada. Nesse exemplo, o modelo é treinado usando clientes com mais de 30 anos que nunca compraram leite.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName='Milk') )  
```  
  

  
###  <a name="bkmk_Ex5"></a> Exemplo 5: Filtrando por vários valores de tabela aninhada  
 O objetivo do exemplo é mostrar a filtragem de tabela aninhada. O filtro da tabela aninhada é aplicado depois do filtro de caso e só restringe as linhas da tabela aninhada.  
  
 Esse modelo pode conter vários casos com tabelas aninhadas vazias porque EXISTS não está especificado.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
WITH DRILLTHROUGH  
```  
  

  
###  <a name="bkmk_Ex6"></a> Exemplo 6: Filtrando por atributos de tabela aninhada e EXISTS  
 Nesse exemplo, o filtro na tabela aninhada restringe as linhas para aquelas que contêm leite ou garrafa de água. Em seguida, os casos no modelo são restringidos usando uma instrução `EXISTS`. Isso garante que a tabela aninhada não está vazia.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
FILTER (EXISTS (Products))  
```  
  

  
###  <a name="bkmk_Ex7"></a> Exemplo 7: Combinações complexas de filtro  
 O cenário desse modelo se assemelha a do Exemplo 4, mas é muito mais complexo. A tabela aninhada, **ProductsOnSale**, tem a condição de filtro `(OnSale)` significando que o valor de **OnSale** deve ser `true` para o produto listado em **ProductName**. Aqui, **OnSale** é uma coluna de estrutura.  
  
 A segunda parte do filtro, para **ProductsNotOnSale**, repete essa sintaxe, mas filtra por produtos para os quais o valor de **OnSale** é `not true``(!OnSale)`.  
  
 Por fim, as condições são combinadas e uma única restrição adicional é adicionada à tabela de casos. O resultado é prever compras de produtos na lista **ProductsNotOnSale** , com base nos casos incluídos na lista **ProductsOnSale** , para todos os clientes com mais de 25 anos.  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
  
  
###  <a name="bkmk_Ex8"></a> Exemplo 8: Filtrando por datas  
 É possível filtrar colunas de entrada por datas, como você faria com qualquer outro dado. As datas contidas em uma coluna de tipo de data/hora são valores contínuos; por isso, é possível especificar um intervalo de datas usando-se operadores como maior que (>) ou menos que (<). Se a fonte de dados não representar datas por um tipo de dados Contínuo, mas como valores discretos ou de texto, não será possível filtrar por um intervalo de datas, e você deverá especificar valores discretos individuais.  
  
 No entanto, não será possível criar um filtro na coluna de data em um modelo de série temporal se a coluna de data usada para o filtro também for a coluna de chave do modelo. Isso porque, em modelos de série temporal e modelos MSC, a coluna de data pode ser manipulada como o tipo `KeyTime` ou `KeySequence`.  
  
 Se precisar filtrar por datas contínuas em um modelo de série temporal, você poderá criar uma cópia da coluna na estrutura de mineração e filtrar o modelo na nova coluna.  
  
 Por exemplo, a expressão a seguir representa um filtro em uma coluna de data do tipo `Continuous` que foi adicionado ao modelo de previsão.  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  Observe que qualquer coluna extra adicionada ao modelo pode afetar os resultados. Por isso, se não quiser usar a coluna na computação da série, você só deverá adicionar a coluna à estrutura de mineração, e não ao modelo. Também é possível definir o sinalizador de modelo na coluna como `PredictOnly` ou `Ignore`. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](modeling-flags-data-mining.md).  
  
 Para outros tipos de modelo, é possível usar datas como critérios de entrada ou de filtro exatamente como você faria em qualquer outra coluna. No entanto, se precisar usar um nível específico de granularidade não suportado por um tipo de dados `Continuous`, você poderá criar um valor derivado na fonte de dados usando expressões para extrair a unidade a ser usada na filtragem e na análise.  
  
> [!WARNING]  
>  Ao especificar uma data como critério de filtro, você deve usar o formato a seguir, independentemente do formato de data do SO atual: `mm/dd/yyyy`. Qualquer outro formato resulta em um erro.  
  
 Por exemplo, se você quiser filtrar os resultados da central de atendimento para mostrar apenas fins de semana, será possível criar uma expressão na exibição da fonte de dados que extrai o nome do dia da semana para cada data e, em seguida, usar o valor do nome desse dia da semana para entrada ou como um valor discreto na filtragem. Basta se lembrar de que, como valores repetidos podem afetar o modelo, você só deve usar uma das colunas, e não a coluna de data mais o valor derivado.  
  
 
  
## <a name="see-also"></a>Consulte também  
 [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-models-analysis-services-data-mining.md)   
 [Teste e validação &#40;Mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
  
