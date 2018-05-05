---
title: Exemplos de consulta de modelo de regressão logística | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- content queries [DMX]
ms.assetid: 7c8e13a3-5c67-46c2-abfa-4881e6ef9c62
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 086104130f865063739773c1813de3c44ef28bc7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="logistic-regression-model-query-examples"></a>Exemplos de consulta de modelo de regressão logística
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ao criar uma consulta para um modelo de mineração de dados, você pode criar uma consulta de conteúdo que fornece detalhes de padrões encontrados em análises ou uma consulta de previsão que usa os padrões no modelo para fazer previsões com os novos dados.  
  
 Esta seção explica como criar consultas para modelos baseados no algoritmo Regressão Logística da Microsoft.  
  
 **Consultas de conteúdo**  
  
 [Recuperando parâmetros de modelo usando o conjunto de linhas do esquema de mineração de dados](#bkmk_Query1)  
  
 [Localizando detalhes adicionais sobre o modelo usando DMX](#bkmk_Query2)  
  
 **Consultas de previsão**  
  
 [Fazendo previsões para um valor contínuo](#bkmk_Query3)  
  
 [Fazendo previsões para um valor discreto](#bkmk_Query4)  
  
##  <a name="bkmk_top"></a> Obtendo informações sobre o Modelo de Regressão Logística  
 Os modelos de regressão logística são criados com o uso do algoritmo Rede Neural da Microsoft com um conjunto especial de parâmetros; portanto, um modelo de regressão logística tem algumas das mesmas informações que um modelo de redes neurais, só que é mais complexo. Para entender a estrutura do conteúdo do modelo e quais tipos de nós armazenam quais tipos de informações, consulte [Mining Model Content for Logistic Regression Models &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
 Para acompanhar os cenários de consulta, você pode criar um modelo de regressão logística conforme descrito na seção seguinte do Tutorial Intermediário de Mineração de Dados: [Lesson 5: Building Neural Network and Logistic Regression Models &#40;Intermediate Data Mining Tutorial&#41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b).  
  
 Você também pode usar a estrutura de mineração, Correspondência destinada, do [Tutorial básico de mineração de dados](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
```  
ALTER MINING STRUCTURE [Targeted Mailing]  
ADD MINING MODEL [TM_Logistic Regression]  
([Customer Key],  
[Age],  
[Bike Buyer] PREDICT,  
[Yearly Income] PREDICT,  
[Commute Distance],  
[English Education],  
Gender,  
[House Owner Flag],  
[Marital Status],  
[Number Cars Owned],  
[Number Children At Home],  
[Region],  
[Total Children]  
)  
USING Microsoft_Logistic_Regression  
```  
  
###  <a name="bkmk_Query1"></a> Exemplo de consulta 1: Recuperando parâmetros de modelos usando o conjunto de linhas do esquema de mineração de dados  
 Ao consultar um conjunto de linhas de esquema de mineração de dados, você pode encontrar metadados sobre o modelo, tais como quando ele foi criado, última vez em que foi processado, o nome da estrutura de mineração na qual o modelo é baseado e o nome da coluna usada como atributo previsível. O exemplo a seguir retorna os parâmetros usados quando o modelo foi criado, junto com o nome e o tipo de modelo, além da data de criação.  
  
```  
SELECT MODEL_NAME, SERVICE_NAME, DATE_CREATED, MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center_LR'  
```  
  
 Resultados do exemplo:  
  
|MODEL_NAME|SERVICE_NAME|DATE_CREATED|MINING_PARAMETERS|  
|-----------------|-------------------|-------------------|------------------------|  
|Call Center_LR|Microsoft_Logistic_Regression|04/07/2009 20:38:33|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=1, MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255, MAXIMUM_STATES=100, SAMPLE_SIZE=10000|  
  
###  <a name="bkmk_Query2"></a> Consulta de exemplo 2: Localizando detalhes adicionais sobre o modelo usando DMX  
 A consulta a seguir retorna algumas informações básicas sobre o modelo de regressão logística. Um modelo de regressão logística é semelhante a um modelo de rede neural em muitos aspectos, inclusive a presença de um nó de estatísticas marginais (NODE_TYPE = 24) que descreve os valores usados como entradas. Esta consulta de exemplo usa o modelo Endereçamento de Destino e obtém os valores de todas as entradas recuperando-as da tabela aninhada, NODE_DISTRIBUTION.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM [TM_Logistic Regression].CONTENT   
```  
  
 Resultados parciais:  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Idade|Ausente|0|0|0|1|  
|Idade|45.43491192|17484|1|126.9544114|3|  
|Bike Buyer|Ausente|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|Distância do Trabalho|Ausente|0|0|0|1|  
|Distância do Trabalho|8-16 quilômetros|3033|0.173472889|0|4|  
  
 A consulta real retorna muito mais linhas; no entanto, este exemplo demonstra o tipo de informações fornecidas sobre as entradas. Para entradas discretas, cada valor possível é listado na tabela. Para entradas de valor contínuo, como Idade, uma listagem completa é impossível, portanto a entrada é de dados discretos como uma média. Para obter mais informações sobre como usar as informações no nó de estatísticas marginais, consulte [Mining Model Content for Logistic Regression Models &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
> [!NOTE]  
>  Os resultados foram simplificados para facilitar a visualização, mas você poderá retornar a tabela aninhada em uma única coluna se seu provedor oferecer suporte a conjuntos de linhas hierárquicos.  
  
## <a name="prediction-queries-on-a-logistic-regression-model"></a>Consultas de previsão em um modelo de regressão logística  
 Você pode usar a função [Predict &#40;DMX&#41;](../../dmx/predict-dmx.md) com todo tipo de modelo de mineração para fornecer dados novos ao modelo e para fazer previsões com base nos novos valores. Também é possível usar funções para retornar mais informações sobre a previsão, como a probabilidade de uma previsão estar correta. Esta seção fornece alguns exemplos de consultas de previsão em um modelo de regressão logística.  
  
###  <a name="bkmk_Query3"></a> Exemplo de consulta 3: Fazendo previsões para um valor contínuo  
 Como a regressão logística também dá suporte ao uso de atributos contínuos para entrada e previsão, é fácil criar modelos que correlacionam vários fatores em seus dados. Você pode usar consultas de previsão para explorar a relação entre esses fatores.  
  
 O exemplo de consulta a seguir é baseado no modelo de Call Center, do Tutorial Intermediário, e cria uma consulta singleton que prevê o nível de serviço do turno matutino da sexta-feira. A função [PredictHistogram (DMX)](../../dmx/predicthistogram-dmx.md) retorna uma tabela aninhada que fornece estatísticas relevantes para entender a validade do valor previsto.  
  
```  
SELECT  
  Predict([Call Center_LR].[Service Grade]) as Predicted ServiceGrade,  
  PredictHistogram([Call Center_LR].[Service Grade]) as [Results],  
FROM  
  [Call Center_LR]  
NATURAL PREDICTION JOIN  
(SELECT 'Friday' AS [Day Of Week],  
  'AM' AS [Shift]) AS t  
```  
  
 Resultados do exemplo:  
  
|Classificação de Serviço Prevista|Nível de serviço|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-----------------------------|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.102601830123659|0.102601830123659|83.0232558139535|0.988372093023256|0|0.00120552660600087|0.034720694203902|  
|||0.976744186046512|0.0116279069767442|0.0116279069767442|0|0|  
  
 Para obter mais informações sobre a probabilidade, suporte e valores de desvio padrão na tabela aninhada NODE_DISTRIBUTION, consulte [Mining Model Content for Logistic Regression Models &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
###  <a name="bkmk_Query4"></a> Exemplo de consulta 4: Fazendo previsões para um valor discreto  
 A regressão logística normalmente é usada em cenários onde você deseja analisar os fatores que contribuem para um resultado binário. Embora o modelo usado no tutorial preveja um valor contínuo, **ServiceGrade**, em um cenário de vida real, você pode desejar configurar o modelo para prever se o nível de serviço atendeu a algum valor de destino de dados discretos. Como alternativa, você pode produzir as previsões usando um valor contínuo, mas posteriormente agrupar os resultados previstos em **Bom**, **Razoável**ou **Fraco**.  
  
 O exemplo a seguir ilustra como alterar a maneira como o atributo previsível é agrupado. Para isso, você cria uma cópia da estrutura de mineração e, em seguida, altera o método de dados discretos da coluna de destino de forma que os valores sejam agrupados em vez de contínuos.  
  
 O procedimento a seguir descreve como alterar o agrupamento de valores de Nível de Serviço nos dados do Call Center.  
  
##### <a name="to-create-a-discretized-version-of-the-call-center-mining-structure-and-models"></a>Para criar uma versão diferenciada da estrutura de mineração e modelos de Call Center  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no Gerenciador de Soluções, expanda **Estruturas de Mineração**.  
  
2.  Clique com o botão direito do mouse em Call Center.dmm e selecione **Copiar**.  
  
3.  Clique com o botão direito em **Estruturas de Mineração** e selecione **Pasta**. Uma nova estrutura de mineração é adicionada, nomeada como Call Center 1.  
  
4.  Clique com o botão direito do mouse na nova estrutura de mineração e selecione **Renomear**. Digite o novo nome, **Dados Discretos do Call Center**.  
  
5.  Clique duas vezes na nova estrutura de mineração para abri-la no designer. Observe que todos os modelos de mineração também foram copiados e que todos têm a extensão 1. Deixe os nomes como estão por enquanto.  
  
6.  Na guia **Estrutura de Mineração** , clique com o botão direito do mouse na coluna Nível de Serviço e selecione **Propriedades**.  
  
7.  Altere a propriedade **Content** de **Contínua** para **Dados Discretos**. Altere a propriedade **DiscretizationMethod** para **Clusters**. Para BucketCount de Dados Discretos, digite **3**.  
  
    > [!NOTE]  
    >  Esses parâmetros são usados apenas para ilustrar o processo e não geram necessariamente um modelo válido.  
  
8.  No menu **Modelo de Mineração** , selecione **Processar estrutura todos os modelos**.  
  
 A consulta de exemplo a seguir é baseada nesse modelo de dados discretos e prevê o nível de serviço durante o dia da semana especificado, junto com as probabilidades de cada resultado previsto.  
  
```  
SELECT  
  (PredictHistogram([Call Center_LR 1].[Service Grade])) as [Predictions]  
FROM  
  [Call Center_LR 1]  
NATURAL PREDICTION JOIN  
(SELECT 'Saturday' AS [Day Of Week]) AS t    
```  
  
 Resultados esperados:  
  
 **Previsões:**  
  
|Nível de serviço|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.10872718383125|35.7246504770641|0.425293458060287|0.0170168360030293|0|0|  
|0.05855769230625|31.7098880800703|0.377498667619885|0.020882020060454|0|0|  
|0.170169491525|15.6109159883202|0.185844237956192|0.0661386571386049|0|0|  
||0.954545454545455|0.0113636363636364|0.0113636363636364|0|0|  
  
 Observe que os resultados previstos foram agrupados em três categorias conforme especificado. No entanto, esses agrupamentos são baseados no clustering de valores reais nos dados, não valores arbitrários que você pode definir como metas comerciais.  
  
## <a name="list-of-prediction-functions"></a>Lista de funções de previsão  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. Entretanto, o algoritmo Regressão Logística da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte às funções adicionais relacionadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|Determina se um nó é um filho de outro nó no modelo.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|Retorna a probabilidade ajustada de um estado especificado.|  
|[PredictHistogram & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|Retorna um valor previsto ou conjunto de valores de uma coluna especificada.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|Retorna a probabilidade para um estado especificado.|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|Retorna o desvio padrão previsto para o valor previsto.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|Retorna o valor de suporte para um estado especificado.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|Retorna a variação de uma coluna especificada.|  
  
 Para obter uma lista das funções comuns a todos os algoritmos [!INCLUDE[msCoName](../../includes/msconame-md.md)], consulte [Funções de previsão gerais &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Para obter a sintaxe de funções específicas, consulte [Referência de função de DMX &#40;extensões DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
> [!NOTE]  
>  Para modelos de rede neural e regressão logística, a função [PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md) retorna um único valor que representa o tamanho do conjunto de treinamento de todo o modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)   
 [Algoritmo de regressão logística da Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Referência técnica do algoritmo de regressão logística de Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de regressão logística & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [Lição 5: Criando Neural Network e modelos de regressão logística & #40; Tutorial de mineração de dados intermediário & #41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  
