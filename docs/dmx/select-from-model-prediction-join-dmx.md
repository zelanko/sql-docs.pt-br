---
title: SELECT FROM &lt;modelo&gt; PREDICTION JOIN (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f0778a104383f54cf2798c0d6f51f082926b1fd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658944"
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM &lt;modelo&gt; PREDICTION JOIN (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Usa um modelo de mineração para predizer os estados de colunas em uma fonte de dados externa. O **PREDICTION JOIN** instrução corresponde a cada caso da consulta de fonte para o modelo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Um inteiro que especifica quantas linhas serão retornadas.  
  
 *Selecione a lista de expressões*  
 Lista separada por vírgula de identificadores e expressões que são derivados de um modelo de mineração.  
  
 *modelo*  
 Identificador de modelo.  
  
 *Selecione sub*  
 Instrução Select inserida.  
  
 *consulta de fonte de dados*  
 Consulta de fonte.  
  
 *lista de mapeamento de junção*  
 Opcional. Expressão lógica que compara colunas do modelo com colunas da consulta de fonte.  
  
 *expressão de condição*  
 Opcional. Uma condição para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 A cláusula ON define o mapeamento entre as colunas da consulta de fonte e as colunas do modelo de mineração. Esse mapeamento é usado para direcionar colunas de uma consulta de fonte para colunas no modelo de mineração, de modo que as colunas possam ser usadas como entradas para criar as previsões. Colunas na \< *lista de mapeamento de junção*> são relacionados por meio de um sinal de igual (=), conforme mostrado no exemplo a seguir:  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 Se você estiver associando uma tabela aninhada à cláusula ON, é preciso verificar se a coluna de chave está associada a qualquer coluna que não seja uma coluna de chave, de modo que o algoritmo possa identificar corretamente a caixa à qual pertence o registro da coluna aninhada.  
  
 A consulta de fonte para a junção de previsão pode ser uma tabela ou uma consulta singleton.  
  
 Você pode especificar funções de previsão que retornam uma expressão de tabela na \< *lista de expressões select*> e o \< *expressão da condição*>.  
  
 **NATURAL PREDICTION JOIN** automaticamente juntos mapeia nomes de coluna da consulta de fonte que correspondem aos nomes de coluna no modelo. Se você usar **previsão NATURAL**, você pode omitir a cláusula ON.  
  
 A condição WHERE só pode ser aplicada a colunas previsíveis ou colunas relacionadas.  
  
 A cláusula ORDER by só pode aceitar uma única coluna como um argumento; ou seja, não é possível classificar em mais de uma coluna.  
  
## <a name="example-1-singleton-query"></a>Exemplo 1: Consulta singleton  
 O exemplo a seguir mostra como criar uma consulta para prever se uma determinada pessoa comprará uma bicicleta em tempo real. Nesta consulta, os dados não são armazenados em uma tabela ou outra fonte de dados, em vez disso, são inseridos diretamente na consulta. A pessoa na consulta tem as seguintes características:  
  
-   35 anos de idade  
  
-   Possui uma casa  
  
-   Possui dois carros  
  
-   Tem dois filhos que moram em casa  
  
 Usando o modelo de mineração de árvore de decisão TM e as características conhecidas sobre o assunto, a consulta retorna um valor booliano que descreve se a pessoa comprou a bicicleta e um conjunto de valores de tabela, retornado pela [PredictHistogram &#40;DMX &#41; ](../dmx/predicthistogram-dmx.md) função, que descrevem como a previsão foi feita.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>Exemplo 2: Usando OPENQUERY  
 O exemplo a seguir mostra como criar uma consulta de previsão em lotes usando uma lista de clientes potenciais armazenada em um conjunto de dados externo. Porque a tabela faz parte de uma exibição da fonte de dados que foi definida em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a consulta pode usar [OPENQUERY](../dmx/source-data-query-openquery.md) para recuperar os dados. Como os nomes das colunas na tabela são diferentes no modelo de mineração, o **ON** cláusula deve ser usada para mapear as colunas na tabela para as colunas no modelo.  
  
 A consulta retorna o primeiro e o último nome de cada pessoa na tabela, junto com uma coluna booliana que indica se cada pessoa provavelmente comprará uma bicicleta, onde 0 significa "provavelmente não comprará uma bicicleta" e 1 significa "provavelmente comprará uma bicicleta". A última coluna contém a probabilidade do resultado previsto.  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [LastName],  
      [FirstName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [Education],  
      [Occupation],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 Para restringir o conjunto de dados apenas aos clientes que provavelmente comprarão uma bicicleta e classificar a lista por nome de cliente, adicione uma cláusula WHERE e uma cláusula ORDER BY ao exemplo anterior:  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>Exemplo 3: Prevendo associações  
 O exemplo a seguir mostra como criar uma previsão usando um modelo que é criado no algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association. As previsões em um modelo de associação podem ser usadas para recomendar produtos relacionados. Por exemplo, a consulta a seguir retorna os três produtos com maior probabilidade de serem adquiridos juntos:  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 O [Predict &#40;DMX&#41; ](../dmx/predict-dmx.md) função é polimórfica e pode ser usada com todos os tipos de modelo. Use value3 como um argumento para a função, para limitar o número de itens retornados pela consulta. O **selecionar** lista que segue a cláusula NATURAL PREDICTION JOIN fornece os valores a serem usados como entrada para previsão.  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 Resultados do exemplo:  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 Como a coluna que contém o atributo previsível `[v Assoc Seq Line Items]` é uma coluna de tabela, a consulta retorna uma única coluna que contém uma tabela aninhada. Por padrão a coluna de tabela aninhada é denominada `Expression`. Se seu provedor não oferece suporte a conjuntos de linhas hierárquicos, você pode usar o **FLATTENED** palavra-chave, conforme mostrado neste exemplo, para facilitar os resultados exibir.  
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
