---
title: Exemplos de consulta de modelo de árvores de decisão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- decision tree algorithms [Analysis Services]
- content queries [DMX]
- decision trees [Analysis Services]
ms.assetid: ceaf1370-9dd1-4d1a-a143-7f89a723ef80
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 009e8d203d9262ee14702b99ad7d0e31d8a16dbb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66084763"
---
# <a name="decision-trees-model-query-examples"></a>Exemplos de consulta de modelo de árvores de decisão
  Ao criar uma consulta para um modelo de mineração de dados, você pode criar uma consulta de conteúdo que fornece detalhes de padrões encontrados em análises ou uma consulta de previsão que usa os padrões no modelo para fazer previsões para novos dados. Por exemplo, uma consulta de conteúdo para um modelo de árvores de decisão pode fornecer estatísticas sobre o número de casos de cada nível da árvore ou as regras que diferenciam os casos. Como alternativa, uma consulta de previsão mapeia o modelo para novos dados para gerar recomendações, classificações e assim sucessivamente. Você também pode recuperar metadados sobre o modelo usando uma consulta.  
  
 Esta seção explica como criar consultas para modelos com base no algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Consultas de conteúdo**  
  
 [Recuperando parâmetros de modelo do conjunto de linhas do esquema de mineração de dados](#bkmk_Query1)  
  
 [Obtendo detalhes sobre árvores no modelo através do DMX](#bkmk_Query2)  
  
 [Recuperando subárvores do modelo](#bkmk_Query3)  
  
 **Consultas de previsão**  
  
 [Retornando previsões com probabilidades](#bkmk_Query4)  
  
 [Prevendo associações de um modelo de árvores de decisão](#bkmk_Query5)  
  
 [Recuperando uma fórmula de regressão de um modelo de árvores de decisão](#bkmk_Query6)  
  
##  <a name="bkmk_top2"></a> Localizando informações sobre o modelo de árvores de decisão  
 Para criar consultas significativas no conteúdo de um modelo de árvores de decisão, você deve compreender a estrutura do conteúdo do modelo e quais tipos de nós armazenam quais tipos de informações. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de árvore de decisão &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query1"></a> Consulta de exemplo 1: Recuperando parâmetros de modelo do conjunto de linhas do esquema de mineração de dados  
 Ao consultar um conjunto de linhas de esquema de mineração de dados, você pode encontrar metadados sobre o modelo, tais como quando ele foi criado, última vez em que foi processado, o nome da estrutura de mineração na qual o modelo é baseado e o nome da coluna usada como atributo previsível. Você também pode retornar os parâmetros que foram usados quando o modelo foi criado.  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 Resultados do exemplo:  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="bkmk_Query2"></a> Consulta de exemplo 2: Retornando detalhes sobre o conteúdo do modelo usando DMX  
 A consulta a seguir retorna algumas informações básicas sobre as árvores de decisão que foram criadas quando o modelo foi construído no [Tutorial de mineração de dados básico](../../tutorials/basic-data-mining-tutorial.md). Cada estrutura de árvore é armazenada em seu próprio nó. Como esse modelo contém um único atributo previsível, há só um nó de árvore. Entretanto, se você criar um modelo de associação usando o algoritmo Árvores de Decisão, pode haver centenas de árvores, uma para cada produto.  
  
 Essa consulta retorna todos os nós de tipo 2, que são os nós superiores de uma árvore que representa um atributo previsível particular.  
  
> [!NOTE]  
>  A coluna `CHILDREN_CARDINALITY` deve estar entre parênteses para distingui-la da palavra-chave reservada MDX de mesmo nome.  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Resultados do exemplo:  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|Todos|12939|5|  
  
 O que esses resultados significam para você? Em um modelo de árvores de decisão, a cardinalidade de um nó específico indica quantos filhos imediatos aquele nó contém. A cardinalidade desse nó é 5, o que indica que o modelo dividiu a população alvo de consumidores de bicicleta em 5 subgrupos.  
  
 A consulta relacionada a seguir retorna os filhos desses cinco subgrupos, juntamente com a distribuição dos atributos e valores nos nós filho. Como as estatísticas, como suporte, probabilidade e variância, são armazenadas na tabela aninhada, `NODE_DISTRIBUTION`, esse exemplo usa a palavra-chave `FLATTENED` para gerar as colunas da tabela aninhada.  
  
> [!NOTE]  
>  A coluna da tabela aninhada, `SUPPORT`, deve estar entre parênteses para distingui-la da palavra-chave reservada de mesmo nome.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 Resultados do exemplo:  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|SUPPORT|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Número de Carros = 0|Bike Buyer|Ausente|0|  
|00000000100|Número de Carros = 0|Bike Buyer|0|1067|  
|00000000100|Número de Carros = 0|Bike Buyer|1|1875|  
|00000000101|Número de Carros = 3|Bike Buyer|Ausente|0|  
|00000000101|Número de Carros = 3|Bike Buyer|0|678|  
|00000000101|Número de Carros = 3|Bike Buyer|1|473|  
  
 Com base nesses resultados, é possível afirmar que dos clientes que compraram uma bicicleta (`[Bike Buyer]` = 1), 1067 clientes não tinham 0 carros e 473 clientes tinham 3 carros.  
  
###  <a name="bkmk_Query3"></a> Consulta de exemplo 3: Recuperando subárvores do modelo  
 Suponha que você queira saber mais sobre os clientes que compraram uma bicicleta. É possível exibir detalhes adicionais para qualquer subárvore usando a função [IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx) na consulta, como mostra o exemplo a seguir. A consulta retorna o cálculo dos compradores de bicicletas recuperando os nós folha (NODE_TYPE = 4) da árvore que contém os clientes acima de 42 anos de idade. A consulta restringe linhas da tabela aninhada para aquelas onde Comprador de Bicicleta = 1.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 Resultados do exemplo:  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Renda Anual >= 26.000 e < 42.000|266|  
|00000000100010100|Total de Filhos = 3|75|  
|0000000010001010100|Número de Crianças em Casa = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>Fazendo previsões com o uso de um modelo de árvores de decisão  
 Como árvores de decisão podem ser usadas em várias tarefas, incluindo classificação, regressão e até mesmo associação, quando você cria uma consulta de previsão em um modelo de árvore de decisão, há muitas opções disponíveis. Você deve entender o propósito para o qual o modelo foi criado para entender os resultados da previsão. Os exemplos de consulta a seguir mostram três cenários diferentes:  
  
-   Retornar uma previsão para um modelo de classificação, juntamente com a probabilidade de a previsão estar correta, e depois filtrar os resultados por probabilidade;  
  
-   Criar uma consulta singleton para prever associações;  
  
-   Recuperar a fórmula de regressão para parte de uma árvore de decisão onde a relação entre a entrada e a saída é linear.  
  
###  <a name="bkmk_Query4"></a> Consulta de exemplo 4: Retornando previsões com probabilidades  
 O exemplo de consulta a seguir usa o modelo de árvore de decisão criado no [Tutorial de mineração de dados básico](../../tutorials/basic-data-mining-tutorial.md). A consulta passa por um novo conjunto de dados de exemplo, da tabela dbo.ProspectiveBuyers em [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW, para prever qual dos clientes do novo conjunto de dados comprará uma bicicleta.  
  
 A consulta usa a função de previsão [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx), que retorna uma tabela aninhada que contém informações úteis sobre as probabilidades encontradas pelo modelo. A cláusula WHERE final da consulta filtra os resultados para retornar apenas os clientes que foram previstos como prováveis compradores de uma bicicleta, com uma probabilidade maior que 0%.  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 Por padrão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna tabelas aninhadas com o nome de coluna, **Expressão**. Você pode alterar esse nome no alias da coluna que é retornada. Se fizer isso, o alias (nesse caso, **Resultados**) será usado no título da coluna e também como valor da tabela aninhada. Você deve expandir a tabela aninhada para verificar os resultados.  
  
 Resultados de exemplo em que o comprador de bicicleta = 1:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|1|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 Se o seu provedor não der suporte a conjuntos de linhas hierárquicos, como os resultados exibidos aqui, você poderá utilizar a palavra-chave FLATTENED na consulta para retornar os resultados em uma tabela que contenha nulos em vez de valores de coluna repetidos. Para obter mais informações, consulte [Tabelas aninhadas &#40;Analysis Services – Data Mining&#41;](nested-tables-analysis-services-data-mining.md) ou [Noções básicas sobre o instrução Select do MDX](/sql/dmx/understanding-the-dmx-select-statement).  
  
###  <a name="bkmk_Query5"></a> Consulta de exemplo 5: Prevendo associações de um modelo de árvores de decisão  
 O exemplo de consulta a seguir é baseado na estrutura de mineração Associação. Para continuar com este exemplo, você pode adicionar um novo modelo a essa estrutura de mineração e selecionar Árvores de Decisão da Microsoft como o algoritmo. Para obter mais informações sobre como criar a estrutura de mineração de associação, consulte [lição 3: Criando um cenário de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md).  
  
 O exemplo de consulta a seguir é uma consulta singleton que pode ser criada facilmente no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] selecionando os campos e depois os valores para esses campos na lista suspensa.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Resultados esperados:  
  
|Modelo|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Tubo de pneu para passeio|  
  
 Os resultados indicam os três melhores produtos para serem recomendados a clientes que compraram o produto Patch Kit. Você também pode fornecer vários produtos como entrada ao fazer suas recomendações, tanto digitando os valores como usando a caixa de diálogo **Entrada de Consulta Singleton** e adicionando ou removendo valores. A consulta de exemplo a seguir mostra como vários valores são fornecidos, sob os quais uma previsão é feita. Os valores são conectados por uma cláusula UNION na instrução SELECT que define os valores de entrada.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Resultados esperados:  
  
|Modelo|  
|-----------|  
|Jersey Logo de manga longa|  
|Mountain-400-W|  
|Colete clássico|  
  
###  <a name="bkmk_Query6"></a> Consulta de exemplo 6: Recuperando uma fórmula de regressão de um modelo de árvores de decisão  
 Ao criar um modelo de árvore de decisão que contém uma regressão em um atributo contínuo, você pode usar a fórmula de regressão para fazer previsões ou pode extrair informações precisas sobre a fórmula. Para obter mais informações sobre consultas em modelos de regressão, consulte [Exemplos de consulta de modelo de regressão linear](linear-regression-model-query-examples.md).  
  
 Se um modelo de árvores de decisão contiver uma mistura de nós de regressão e esses nós se dividirem em atributos discretos ou intervalos, você poderá criar uma consulta que retorne apenas o nó de regressão. A tabela NODE_DISTRIBUTION contém os detalhes da fórmula de regressão. Neste exemplo, as colunas são combinadas e a tabela NODE_DISTRIBUTION recebe um alias para facilitar a exibição. Porém, neste modelo, nenhum regressor foi localizado para relacionar Renda com outros atributos contínuos. Nesses casos, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna o valor médio do atributo e a variância total no modelo para aquele atributo.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 Resultados do exemplo:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Renda Anual|Ausente|0|0.000457142857142857|0|1|  
|Renda Anual|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
||57220.8876687257|0|0|1041216662.54387|11|  
  
 Para obter mais informações sobre os tipos de valor e as estatísticas usadas nos modelos de regressão, consulte [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
## <a name="list-of-prediction-functions"></a>Lista de funções de previsão  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. Entretanto, o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] dá suporte a funções adicionais relacionadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Determina se um nó é um filho de outro nó no modelo.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se o nó especificado contém o caso atual.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Retorna a probabilidade ponderada.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Prevê associação de membro em um conjunto de dados associativo.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Retorna uma tabela de valores relacionados ao valor previsto atual.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Retorna Node_ID para cada caso.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Retorna a probabilidade para o valor previsto.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Retorna o desvio padrão previsto para a coluna especificada.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Retorna o valor de suporte para um estado especificado.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Retorna a variação de uma coluna especificada.|  
  
 Para obter uma lista das funções comuns a todos os algoritmos [!INCLUDE[msCoName](../../includes/msconame-md.md)], consulte [Funções de previsão gerais &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx). Para obter a sintaxe de funções específicas, consulte [Referência de função de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de mineração de dados](data-mining-queries.md)   
 [Algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm.md)   
 [Referência técnica do algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de árvore de decisão &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
