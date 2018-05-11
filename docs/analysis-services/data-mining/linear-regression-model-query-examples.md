---
title: Exemplos de consulta de modelo de regressão linear | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e015b75e5b1e8b6e6bfb267fee7546ff8b4d0d9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="linear-regression-model-query-examples"></a>Exemplos de consulta de modelo de regressão linear
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ao criar uma consulta para um modelo de mineração de dados, você pode criar uma consulta de conteúdo que fornece detalhes de padrões encontrados em análises ou uma consulta de previsão que usa os padrões no modelo para fazer previsões para novos dados. Por exemplo, uma consulta de conteúdo pode fornecer mais detalhes sobre a fórmula de regressão, enquanto uma consulta de previsão pode informar se um novo ponto de dados se ajusta ao modelo. Você também pode recuperar metadados sobre o modelo usando uma consulta.  
  
 Esta seção explica como criar consultas para modelos baseados no algoritmo Regressão Linear da Microsoft.  
  
> [!NOTE]  
>  Como a regressão linear se baseia em um caso especial do algoritmo Árvores de Decisão da Microsoft, há muitas semelhanças. Além disso, alguns modelos de árvore de decisão que usam atributos previsíveis contínuos podem conter fórmulas de regressão. Para obter mais informações, consulte [Referência técnica do algoritmo Árvores de Decisão da Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md).  
  
 **Consultas de conteúdo**  
  
 [Usando o conjunto de linhas de esquema de mineração de dados para determinar parâmetros usados para um modelo](#bkmk_Query1)  
  
 [Usando o DMX para retornar a fórmula de regressão do modelo](#bkmk_Query2)  
  
 [Retornando apenas o coeficiente do modelo](#bkmk_Query3)  
  
 **Consultas de previsão**  
  
 [Prevendo o resultado com o uso de uma consulta singleton](#bkmk_Query4)  
  
 [Usando funções de previsão com um modelo de regressão](#bkmk_Query5)  
  
##  <a name="bkmk_top"></a> Localizando informações sobre o modelo de regressão linear  
 A estrutura de um modelo de regressão linear é extremamente simples: o modelo de mineração representa os dados como um único nó, que define a fórmula de regressão. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de regressão logística &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
 [Retornar ao início](#bkmk_top)  
  
###  <a name="bkmk_Query1"></a> Exemplo de consulta 1: Usando o conjunto de linhas de esquema de mineração de dados para determinar parâmetros usados para um modelo  
 Ao consultar o conjunto de linhas do esquema de mineração de dados, você pode encontrar metadados sobre o modelo. Isso pode incluir quando o modelo foi criado, quando o modelo foi processado pela última vez, o nome da estrutura de mineração na qual o modelo se baseia e o nome da coluna designada como o atributo previsível. Você também pode retornar os parâmetros que foram usados quando o modelo foi criado.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_PredictIncome'  
```  
  
 Resultados do exemplo:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY=0.9,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES = 255<br /><br /> MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MINIMUM_SUPPORT = 10<br /><br /> SCORE_METHOD=4,<br /><br /> SPLIT_METHOD=3,<br /><br /> FORCE_REGRESSOR=|  
  
> [!NOTE]  
>  A configuração de parâmetro "`FORCE_REGRESSOR =` " indica que o valor atual do parâmetro FORCE_REGRESSOR é nulo.  
  
 [Retornar ao início](#bkmk_top)  
  
###  <a name="bkmk_Query2"></a> Exemplo de consulta 2: Recuperando a fórmula de regressão do modelo  
 A consulta a seguir retorna o conteúdo do modelo de mineração de um modelo de regressão linear criado com o uso dos mesmos dados de Mala Direta utilizados no [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Este modelo prevê a renda do cliente com base na idade.  
  
 A consulta retorna o conteúdo do nó que contém a fórmula de regressão. Cada variável e coeficiente são armazenados em uma linha separada da tabela aninhada NODE_DISTRIBUTION. Para exibir a fórmula de regressão completa, use o [Visualizador de Árvore da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md), clique no nó **(Tudo)** e abra a **Legenda de Mineração**.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION as t  
FROM LR_PredictIncome.CONTENT  
```  
  
> [!NOTE]  
>  Se você referenciar colunas individuais da tabela aninhada usando uma consulta como `SELECT <column name> from NODE_DISTRIBUTION`, algumas colunas, como **SUPPORT** ou **PROBABILITY**, deverão ser colocadas entre colchetes para distingui-las das palavras-chave reservadas de mesmo nome.  
  
 Resultados esperados:  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Renda Anual|Ausente|0|0.000457142857142857|0|1|  
|Renda Anual|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|Idade|471.687717702463|0|0|126.969442359327|7|  
|Idade|234.680904692439|0|0|0|8|  
|Idade|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 Em comparação, na **Legenda de Mineração**, a fórmula de regressão aparece da seguinte forma:  
  
 `Yearly Income = 57,220.919 + 471.688 * (Age - 45.427)`  
  
 Você pode observar que, na **Legenda de Mineração**, alguns números são arredondados; no entanto, a tabela NODE_DISTRIBUTION e a **Legenda de Mineração** contêm basicamente os mesmos valores.  
  
 Os valores na coluna VALUETYPE informa que tipo de informações estão em cada linha, o que será útil se você estiver processando os resultados programaticamente. A tabela a seguir mostra os tipos de valores produzidos para uma fórmula de regressão linear.  
  
|VALUETYPE|  
|---------------|  
|1 (Ausente)|  
|3 (Contínuo)|  
|7 (Coeficiente)|  
|8 (Ganho de pontos)|  
|9 (Estatísticas)|  
|7 (Coeficiente)|  
|8 (Ganho de pontos)|  
|9 (Estatísticas)|  
|11 (Interceptação)|  
  
 Para obter mais informações sobre o significado de cada tipo de valor para modelos de regressão, consulte [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
 [Retornar ao início](#bkmk_top)  
  
###  <a name="bkmk_Query3"></a> Exemplo de consulta 3: Retornando apenas o coeficiente do modelo  
 Ao usar a enumeração VALUETYPE, você só pode retornar o coeficiente da equação de regressão, conforme mostrado na seguinte consulta:  
  
```  
SELECT FLATTENED MODEL_NAME,  
    (SELECT ATTRIBUTE_VALUE, VALUETYPE  
     FROM NODE_DISTRIBUTION  
     WHERE VALUETYPE = 11)   
AS t  
FROM LR_PredictIncome.CONTENT  
```  
  
 Essa consulta retorna duas linhas, um a do conteúdo do modelo de mineração e a outra da tabela aninhada que contém o coeficiente. A coluna ATTRIBUTE_NAME não é incluída aqui porque sempre fica em branco para o coeficiente.  
  
|MODEL_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|-----------------|------------------------|-----------------|  
|LR_PredictIncome|||  
|LR_PredictIncome|35793.5477381267|11|  
  
 [Retornar ao início](#bkmk_top)  
  
## <a name="making-predictions-from-a-linear-regression-model"></a>Fazendo previsões de um modelo de regressão linear  
 Você pode criar consultas de previsão em modelos de regressão linear usando a guia Previsão do Modelo de Mineração no Designer de Mineração de Dados. O construtor de consultas de previsão está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Também é possível criar consultas em modelos de regressão usando os Suplementos de Mineração de Dados para Excel do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] . Mesmo que os Suplementos de Mineração de Dados para Excel não criem modelos de regressão, você pode procurar e consultar qualquer modelo de mineração armazenado em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 [Retornar ao início](#bkmk_top)  
  
###  <a name="bkmk_Query4"></a> Exemplo de consulta 4: Prevendo a renda com o uso de uma consulta singleton  
 A maneira mais fácil de criar uma consulta single em um modelo de regressão é usando a caixa de diálogo **Entrada de Consulta Singleton** . Por exemplo, você pode criar a consulta DMX a seguir selecionando o modelo de regressão apropriado, escolhendo **Consulta Singleton**e depois digitando **20** como o valor de **Idade**.  
  
```  
SELECT [LR_PredictIncome].[Yearly Income]  
From   [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 Resultados do exemplo:  
  
|Renda Anual|  
|-------------------|  
|45227.302092176|  
  
 [Retornar ao início](#bkmk_top)  
  
###  <a name="bkmk_Query5"></a> Exemplo de consulta 5: Usando funções de previsão com um modelo de regressão  
 Você pode usar muitas das funções de previsão padrão com modelos de regressão linear. O exemplo a seguir demonstra como adicionar algumas estatísticas descritivas aos resultados da consulta de previsão. Com base nesses resultados, você pode observar que há um desvio considerável da média para este modelo.  
  
```  
SELECT  
  ([LR_PredictIncome].[Yearly Income]) as [PredIncome],  
  (PredictStdev([LR_PredictIncome].[Yearly Income])) as [StDev1]  
From  
  [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 Resultados do exemplo:  
  
|Renda Anual|StDev1|  
|-------------------|------------|  
|45227.302092176|31827.1726561396|  
  
 [Retornar ao início](#bkmk_top)  
  
## <a name="list-of-prediction-functions"></a>Lista de funções de previsão  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. Entretanto, o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte às funções adicionais relacionadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|Determina se um nó é um filho de outro nó no modelo.|  
|[IsInNode & #40; DMX & #41;](../../dmx/isinnode-dmx.md)|Indica se o nó especificado contém o caso atual.|  
|[PredictHistogram & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|Retorna um valor previsto ou conjunto de valores de uma coluna especificada.|  
|[PredictNodeId & #40; DMX & #41;](../../dmx/predictnodeid-dmx.md)|Retorna Node_ID para cada caso.|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|Retorna o desvio padrão previsto para o valor previsto.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|Retorna o valor de suporte para um estado especificado.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|Retorna a variação de uma coluna especificada.|  
  
 Para obter uma lista das funções comuns a todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)], consulte [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md). Para obter mais informações sobre como usar essas funções, consulte [Referência de função de DMX &#40;extensões DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo de regressão Linear da Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)   
 [Referência técnica do algoritmo de regressão Linear de Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de regressão Linear & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
