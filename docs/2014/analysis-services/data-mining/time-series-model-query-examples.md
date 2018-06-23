---
title: Exemplos de consulta de modelo de série temporal | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- time series algorithms [Analysis Services]
- MISSING_VALUE_SUBSTITUTION
- time series [Analysis Services]
- predictions [Analysis Services], time series
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- prediction queries [DMX]
- PREDICTION_SMOOTHING
- content queries [DMX]
ms.assetid: 9a1c527e-2997-493b-ad6a-aaa71260b018
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8b6c0f25f4d5694d678e51acc0ecb4ccbf98f8a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115571"
---
# <a name="time-series-model-query-examples"></a>Exemplos de consulta de um modelo de série temporal
  Ao criar uma consulta para um modelo de mineração de dados, você pode criar uma consulta de conteúdo, que fornece detalhes de padrões descobertos em análises, ou uma consulta de previsão, que usa os padrões no modelo para fazer previsões para novos dados. Por exemplo, uma consulta de conteúdo para um modelo de série temporal pode fornecer detalhes adicionais sobre as estrutura periódicas encontradas, enquanto uma consulta de previsão pode informar as previsões para as próximas 5-10 frações de tempo. Você também pode recuperar metadados sobre o modelo usando uma consulta.  
  
 Esta seção explica como criar ambos os tipos de consultas para modelos que se baseiam no algoritmo MTS.  
  
 **Consultas de conteúdo**  
  
 [Recuperando dicas de periodicidade do modelo](#bkmk_Query1)  
  
 [Recuperando a equação para um modelo ARIMA](#bkmk_Query2)  
  
 [Recuperando a equação para um modelo ARTxp](#bkmk_Query3)  
  
 **Consultas de previsão**  
  
 [Compreendendo quando substituir e quando estender dados de série temporal](#bkmk_ReplaceExtend)  
  
 [Fazendo previsões com EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [Fazendo previsões com REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
 [Substituição de valor ausente em modelos de série temporal](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>Obtendo informações sobre um modelo de série temporal  
 Uma consulta de conteúdo de modelo fornece informações básicas sobre o modelo, como parâmetros usados quando o modelo foi criado e a última vez que o modelo foi processado. O exemplo a seguir ilustra a sintaxe básica para consultar o conteúdo do modelo usando os conjuntos de linhas de esquema de mineração de dados.  
  
###  <a name="bkmk_Query1"></a> Exemplo de consulta 1: Recuperando dicas de periodicidade do modelo  
 Você pode recuperar as periodicidades encontradas em uma série de dados ao consultar o árvore ARIMA ou ARTXP. Entretanto, as periodicidades em um modelo completo podem não ser as mesmas especificadas como dicas ao criar o modelo. Para recuperar as dicas fornecidas como parâmetros ao criar o modelo, você pode consultar o conjunto de linhas de esquema do conteúdo do modelo de mineração usando a seguinte instrução DMX:  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 Resultados parciais:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY = 0,1, MINIMUM_SUPPORT = 10, PERIODICITY_HINT ={1,3},...|  
  
 A dica de periodicidade padrão é {1} e aparece em todos os modelos. Esse modelo de exemplo foi criado com uma dica adicional que pode não estar presente no final do modelo.  
  
> [!NOTE]  
>  Os resultados foram truncados aqui para legibilidade.  
  
###  <a name="bkmk_Query2"></a> Exemplo de consulta 2: Recuperando a equação para um modelo ARIMA  
 Você pode recuperar a equação para um modelo ARIMA consultando qualquer nó em uma árvore individual. Lembre-se de que cada árvore em um modelo ARIMA representa uma periodicidade diferente; se houver várias séries de dados, cada série terá seu próprio conjunto de árvores de periodicidade. Sendo assim, para recuperar a equação para uma série de dados específica, você deve primeiramente identificar a árvore.  
  
 Por exemplo, o prefixo TA indica que o nó faz parte de uma árvore ARIMA, enquanto que o prefixo TS é usado para árvores ARTXP. É possível localizar todas as árvores de raiz ARIMA consultando o conteúdo do modelo para nós com um NODE_TYPE de valor 27. Você também pode usar o valor ATTRIBUTE_NAME para localizar o nó raiz ARIMA para uma série de dados em particular. Este exemplo de consulta localiza os nós ARIMA que representam quantidades vendidas do modelo R250 na região Europa.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 Ao usar essa ID de nó, você poderá recuperar detalhes sobre a equação ARIMA dessa árvore. A instrução DMX a seguir recupera a forma reduzida da equação ARIMA para a série de dados. Ela também recupera a interceptação da tabela aninhada, NODE_DISTRIBUTION. Neste exemplo, a equação é obtida pela referenciação da ID exclusiva do nó, TA00000007. No entanto, talvez seja preciso usar uma ID do nó diferente e obter resultados ligeiramente diferentes do seu modelo.  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 Resultados do exemplo:  
  
|Equação reduzida|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24….|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 Para obter mais informações sobre como interpretar essas informações, consulte [Mining Model Content for Time Series Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query3"></a> Exemplo de consulta 3: Recuperando a equação para um modelo ARTXP  
 No caso de um modelo ARTxp, informações diferentes são armazenadas a cada nível da árvore. Para obter mais informações sobre a estrutura de um modelo ARTxp e como interpretar as informações na equação, consulte [Mining Model Content for Time Series Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 A instrução DMX a seguir recupera informações como parte da árvore ARTxp para a série que representa a quantidade do modelo R250 vendida na região Europa.  
  
> [!NOTE]  
>  O nome da coluna da tabela aninhada, VARIANCE, deve estar entre colchetes para distingui-lo da palavra-chave reservada de mesmo nome. As colunas da tabela aninhada, PROBABILITY e SUPPORT, não são incluídas porque estão vazias na maioria dos casos.  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 Para obter mais informações sobre como interpretar essas informações, consulte [Mining Model Content for Time Series Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
## <a name="creating-predictions-on-a-time-series-model"></a>Criando previsões em um modelo de série temporal  
 Começando no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)], é possível adicionar novos dados ao modelo de série temporal e incorporar automaticamente os novos dados no módulo. Você adiciona novos dados a um modelo de mineração de série temporal de um de dois modos:  
  
-   Use um `PREDICTION JOIN` para unir dados em uma fonte externa para os dados de treinamento.  
  
-   Use uma consulta de previsão singleton para fornecer dados para uma fatia de cada vez. Para obter informações sobre como criar uma consulta de previsão singleton, consulte [Interfaces de consulta de mineração de dados](data-mining-query-tools.md).  
  
###  <a name="bkmk_ReplaceExtend"></a> Entendendo o comportamento de operações de substituir e estender  
 Ao adicionar novos dados a um modelo de série temporal, é possível especificar se deseja estender ou substituir os dados de treinamento:  
  
-   **Estender:** Quando você estende uma série de dados, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adiciona os novos dados no final dos dados de treinamento existentes. O número de casos de treinamento também aumenta.  
  
     Estender os casos de modelo é útil para atualizar o modelo continuamente com dados novos. Por exemplo, se desejar fazer o conjunto de treinamento crescer com o tempo, bastará estender o modelo.  
  
     Para estender os dados, você cria um `PREDICTION JOIN` em um modelo de série temporal, especifique a origem dos novos dados e usar o `EXTEND_MODEL_CASES` argumento.  
  
-   **Substituir:** Quando você substitui os dados na série de dados, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantém o modelo treinado, mas usa os novos valores de dados para substituir alguns ou todos os casos de treinamento existentes. Portanto, o tamanho dos dados de treinamento nunca muda, mas os casos em si estão continuamente sendo substituídos com dados mais novos. Se você fornecer dados novos suficientes, será possível substituir os dados de treinamento com uma série completamente nova.  
  
     Substituir os casos de modelo é útil quando você desejar treinar um modelo em um conjunto de casos e, então, aplicar o modelo a uma série de dados diferente.  
  
     Para substituir os dados, você cria uma `PREDICTION JOIN` em um modelo de série temporal, especifica a origem dos novos dados e usa o argumento `REPLACE_MODEL_CASES`.  
  
> [!NOTE]  
>  Não é possível fazer previsões históricas quando você adiciona novos dados.  
  
 Independentemente de você estender ou substituir os dados de treinamento, as previsões sempre começam no carimbo de data e hora que encerra o conjunto de treinamento original. Em outras palavras, se os seus novos dados contiverem n frações de tempo e você solicitar previsões para os períodos de 1 a n, as previsões coincidirão com o mesmo período dos novos dados e nenhuma previsão nova será obtida.  
  
 Para obter previsões novas para períodos não sobrepostos aos dados novos, você deverá iniciar as previsões na fração de tempo n + 1 ou não se esquecer de solicitar frações de tempo adicionais.  
  
 Por exemplo, suponha que o modelo existente possua seis de meses de dados. Você deseja estender esse modelo adicionando os valores de vendas dos últimos três meses. Ao mesmo tempo, você quer fazer uma previsão sobre os próximos três meses. Para obter apenas as previsões novas ao adicionar os novos dados, especifique o ponto de partida como fração de tempo 4 e o ponto final como fração de tempo 7. Você também pode solicitar um total de seis previsões, mas as frações de tempo para as três primeiras seriam sobrepostas com os novos dados recém-adicionados.  
  
 Para obter exemplos de consulta e obter mais informações sobre a sintaxe para usar `REPLACE_MODEL_CASES` e `EXTEND_MODEL_CASES`, consulte [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="bkmk_EXTEND"></a> Fazendo previsões com EXTEND_MODEL_CASES  
 O comportamento de previsão difere dependendo se você estende ou substitui os casos de modelo. Quando você estende um modelo, os novos dados são anexados ao fim da série e o tamanho do conjunto de treinamento aumenta. Porém, as frações de tempo usadas para consultas de previsão sempre iniciam no término da série original. Portanto, se você adicionar três novos pontos de dados e solicitar seis previsões, as três primeiras previsões retornariam sobrepostas com os novos dados. Nesse caso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna os pontos de dados novos reais ao invés de fazer uma previsão, até que os novos pontos de dados sejam usados. Então, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] faz previsões com base na série composta.  
  
 Esse comportamento permite a você adicionar novos dados e, em seguida, exibir os valores de vendas reais no gráfico da previsão, ao invés de fazer projeções.  
  
 Por exemplo, para adicionar três pontos de dados novos e fazer três previsões novas, você deveria fazer o seguinte:  
  
-   Criar uma `PREDICTION JOIN` em um modelo de série temporal e especificar a origem dos três meses de dados novos.  
  
-   Solicitar previsões para seis frações de tempo. Para isso, especifique 6 frações de tempo, onde o ponto de partida é 1 e o ponto final é a fração de tempo 7. Isso só é verdadeiro para EXTEND_MODEL_CASES.  
  
-   Para obter apenas as previsões novas, especifique o ponto de partida como 4 e o ponto final como 7.  
  
-   Você deve usar o argumento `EXTEND_MODEL_CASES`.  
  
     Os valores reais de vendas são retornados nas três primeiras frações de tempo e as previsões com base no modelo estendido são retornadas para as próximas três frações de tempo.  
  
###  <a name="bkmk_REPLACE"></a> Fazendo previsões com REPLACE_MODEL_CASES  
 Quando você substitui os casos em um modelo, o tamanho do modelo sempre permanece o mesmo, mas o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] substitui os casos individuais no modelo. Isso é útil em previsões cruzadas e cenários em que manter o conjunto de dados de treinamento em um tamanho consistente é importante.  
  
 Por exemplo, uma de suas lojas tem insuficientes dados de vendas. Você poderia criar um modelo geral pela média de vendas para todas as lojas em uma determinada região e, em seguida, treinar um modelo. Em seguida, para fazer previsões para a loja sem dados de vendas suficientes, você cria um `PREDICTION JOIN` sobre os novos dados de vendas apenas dessa loja. Ao fazer isso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantém os padrões derivados do modelo regional, mas substitui os casos de treinamento existentes com os dados da loja individual. Como resultado, os valores de sua previsão serão mais próximos às linhas de tendência para a loja individual.  
  
 Quando você usa o argumento `REPLACE_MODEL_CASES`, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adiciona continuamente novos casos ao fim do conjunto de casos e exclui o número correspondente do inicio do conjunto de casos. Se você adicionar mais dados novos do que havia no conjunto de treinamento original, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta os dados mais antigos. Se você fornecer valores novos suficientes, as previsões poderão ser fundadas em dados completamente novos.  
  
 Por exemplo, você treinou seu modelo em um conjunto de dados de caso que continha 1000 linhas. Então você adiciona 100 linhas de dados novos. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta as primeiras 100 linhas do conjunto de treinamento e adicionas as 100 linhas de dados novos no final do conjunto para um total de 1000 linhas. Se você adicionar 1100 linhas de dados novos, só as 1000 linhas mais recentes serão usadas.  
  
 Segue mais um exemplo. Para adicionar os valores de três meses de dados novos e fazer três previsões novas, você deveria executar as seguintes ações:  
  
-   Criar um `PREDICTION JOIN` em um modelo de série temporal e usar o argumento `REPLACE_MODEL_CASE`.  
  
-   Especificar a fonte de três meses de dados novos. Tais dados poderiam ser de uma fonte completamente diferente que os dados de treinamento originais.  
  
-   Solicitar previsões para seis frações de tempo. Para isso, especifique 6 frações de tempo ou especifique o ponto de partida como fração de tempo 1 e o ponto final como fração de tempo 7.  
  
    > [!NOTE]  
    >  Diferentemente do`EXTEND_MODEL_CASES`, você não pode retornar os mesmos valores que você adicionou como dados de entrada. Todos os seis valores retornados são previsões baseadas no modelo atualizado, que inclui os dados novos e antigos.  
  
    > [!NOTE]  
    >  Com REPLACE_MODEL_CASES, iniciar no timestamp 1 fornece novas previsões com base em novos dados que substituem os dados de treinamento antigos.  
  
 Para obter exemplos de consulta e obter mais informações sobre a sintaxe para usar `REPLACE_MODEL_CASES` e `EXTEND_MODEL_CASES`, consulte [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="bkmk_MissingValues"></a> Substituição de valor ausente em modelos de série temporal  
 Ao adicionar novos dados em um modelo de série temporal usando uma instrução `PREDICTION JOIN`, o novo conjunto de dados não poderá ter dados ausentes. Se qualquer série estiver incompleta, o modelo deverá fornecer os valores ausentes usando um valor nulo, uma média numérica, uma média numérica específica ou um valor previsto. Se você especificar o `EXTEND_MODEL_CASES`, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] substituirá os valores ausentes com previsões baseadas no modelo original. Se você usar `REPLACE_MODEL_CASES`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] substitui os valores ausentes com o valor que você especificar o *MISSING_VALUE_SUBSTITUTION* parâmetro.  
  
## <a name="list-of-prediction-functions"></a>Lista de funções de previsão  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. Entretanto, o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series oferece suporte às funções adicionais relacionadas na tabela a seguir:  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[Latência &#40;DMX&#41;](/sql/dmx/lag-dmx)|Retorna várias frações de tempo entre a data do caso atual e a última data do conjunto de treinamento.<br /><br /> Um uso típico dessa função é para identificar casos recentes de treinamento, de forma que você possa recuperar dados detalhados sobre os casos.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Retorna o identificador do nó para a coluna previsível especificada.<br /><br /> Um uso típico dessa função é para identificar o nó que gerou um valor previsto específico, de forma que você possa revisar os casos associados ao nó ou recuperar a equação e outros detalhes.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Retorna o desvio padrão das previsões na coluna previsível especificada.<br /><br /> Essa função substitui o argumento INCLUDE_STATISTICS, para o qual não há suporte nos modelos da série temporal.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Retorna a variação das previsões na coluna previsível especificada.<br /><br /> Essa função substitui o argumento INCLUDE_STATISTICS, para o qual não há suporte nos modelos da série temporal.|  
|[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)|Retorna valores de histórico previstos ou futuros para os dados da série temporal.<br /><br /> Você também pode consultar os modelos de série temporal usando a função de previsão geral [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx).|  
  
 Para obter uma lista das funções comuns a todos os algoritmos [!INCLUDE[msCoName](../../includes/msconame-md.md)], consulte [Funções de previsão gerais &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx). Para obter a sintaxe de funções específicas, consulte [Referência de função de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de mineração de dados](data-mining-queries.md)   
 [Algoritmo MTS](microsoft-time-series-algorithm.md)   
 [Referência técnica do algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md)   
 [Conteúdo do modelo para modelos de série temporal mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
