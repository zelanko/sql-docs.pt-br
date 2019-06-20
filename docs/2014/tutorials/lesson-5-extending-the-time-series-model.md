---
title: 'Lição 5: Estendendo a série temporal de modelo | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7aad4946-c903-4e25-88b9-b087c20cb67d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2716e985897f8115d189d9410b7cdb13fb1af291
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62822054"
---
# <a name="lesson-5-extending-the-time-series-model"></a>Lição 5: Como estender o modelo de série temporal
  No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise, é possível adicionar novos dados a um modelo de série temporal e incorporar automaticamente os novos dados no módulo. Você adiciona novos dados a um modelo de mineração de série temporal de um de dois modos:  
  
-   Use PREDICTION JOIN para unir dados em uma fonte externa para os dados de treinamento.  
  
-   Use uma consulta de previsão singleton para fornecer dados para uma fatia de cada vez.  
  
 Por exemplo, suponha que você treinou o modelo de mineração em dados de vendas existentes há alguns meses. Ao fazer novas vendas, talvez você queira atualizar as previsões de vendas para incorporá-las aos novos dados. É possível fazer isso em uma etapa, fornecendo os novos números de vendas como dados de entrada e gerando novas previsões baseadas no conjunto de dados composto.  
  
## <a name="making-predictions-with-extendmodelcases"></a>Fazendo previsões com EXTEND_MODEL_CASES  
 A seguir, exemplos genéricos de uma previsão de série temporal usando EXTEND_MODEL_CASES. O primeiro exemplo permite que você especifique o número de previsões, começando pelo último período do modelo original:  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>]  
```  
  
 O segundo exemplo permite que você especifique o período onde as previsões devem começar e onde devem terminar. Essa opção é importante quando você estende os casos do modelo já que, por padrão, os períodos usados para consultas de previsão sempre iniciam no término da série original.  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n-start, n-end, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>}  
```  
  
 Neste tutorial, você criará ambos os tipos de consultas.  
  
#### <a name="to-create-a-singleton-prediction-query-on-a-time-series-model"></a>Como criar uma consulta de previsão singleton em um modelo de série temporal  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução singleton, no campo em branco da consulta.  
  
3.  Substitua o seguinte:  
  
    ```  
    SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
    ```  
  
     por:  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    ```  
  
     A primeira linha recupera um valor do modelo que identifica a série.  
  
     A segunda linha contém a função de previsão, que obtém 6 previsões para Quantidade. Um alias, `PredictQty`, é atribuído à coluna de resultados da previsão para facilitar a compreensão dos resultados.  
  
4.  Substitua o seguinte:  
  
    ```  
    FROM <mining model>  
    ```  
  
     por:  
  
    ```  
    FROM [Forecasting_MIXED]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    PREDICTION JOIN <source query>  
    ```  
  
     por:  
  
    ```  
    NATURAL PREDICTION JOIN   
    (  
       SELECT 1 AS [Reporting Date],  
       '10' AS [Quantity],  
       'M200 Europe' AS [Model Region]  
       UNION SELECT  
       2 AS [Reporting Date],  
       15 AS [Quantity]),  
       'M200 Europe' AS [Model Region]  
    ) AS t  
    ```  
  
6.  Substitua o seguinte:  
  
    ```  
    [WHERE <criteria>]  
    ```  
  
     por:  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    FROM  
       [Forecasting_MIXED]  
    NATURAL PREDICTION JOIN   
       SELECT 1 AS [ReportingDate],  
      '10' AS [Quantity],  
      'M200 Europe' AS [ModelRegion]  
    UNION SELECT  
      2 AS [ReportingDate],  
      15 AS [Quantity]),  
      'M200 Europe' AS [ModelRegion]  
    ) AS t  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
7.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
8.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Singleton_TimeSeries_Query.dmx`.  
  
9. Na barra de ferramentas, clique o **Execute** botão.  
  
     A consulta retorna previsões de quantidade de vendas para as bicicletas M200 na Europa e nas regiões do Pacífico.  
  
## <a name="understanding-prediction-start-with-extendmodelcases"></a>Compreendendo o início das previsões com EXTEND_MODEL_CASES  
 Agora que você criou previsões com base no modelo original, e com novos dados, poderá comparar os resultados para ver como a atualização dos dados de vendas afeta as previsões. Antes disso, examine o código recém-criado e observe o seguinte:  
  
-   Você só forneceu novos dados para a região da Europa.  
  
-   Você só forneceu novos dados relativos a dois meses.  
  
 A tabela a seguir mostra como os novos valores fornecidos para a M200 na Europa afetam as previsões. Você não forneceu dados novos para o produto M200 na região do Pacífico, mas essa série será apresentada para fins de comparação:  
  
 **Produto e região: M200 Europa**  
  
|||||  
|-|-|-|-|  
|||Modelo existente (`PredictTimeSeries`)|Modelo com dados de vendas atualizados (`PredictTimeSeries` com `EXTEND_MODEL_CASES`)|  
|M200 Europa|7/25/2008 12:00:00 AM|77|10|  
|M200 Europa|8/25/2008 12:00:00 AM|64|15|  
|M200 Europa|9/25/2008 12:00:00 AM|59|72|  
|M200 Europa|10/25/2008 12:00:00 AM|56|69|  
|M200 Europa|11/25/2008 12:00:00 AM|56|68|  
|M200 Europa|12/25/2008 12:00:00 AM|74|89|  
  
 **Produto e região: M200 Pacific**  
  
|||||  
|-|-|-|-|  
|||Modelo existente (`PredictTimeSeries`)|Modelo com dados de vendas atualizados (`PredictTimeSeries` com `EXTEND_MODEL_CASES`)|  
|M200 Pacífico|7/25/2008 12:00:00 AM|41|41|  
|M200 Pacífico|8/25/2008 12:00:00 AM|44|44|  
|M200 Pacífico|9/25/2008 12:00:00 AM|38|38|  
|M200 Pacífico|10/25/2008 12:00:00 AM|41|41|  
|M200 Pacífico|11/25/2008 12:00:00 AM|36|36|  
|M200 Pacífico|12/25/2008 12:00:00 AM|39|39|  
  
 A partir desses resultados, você pode observar dois aspectos:  
  
-   As duas primeiras previsões para a série M200 Europe são exatamente iguais aos novos dados fornecidos. Por design, o Analysis Services retorna os pontos de dados novos reais em vez de fazer uma previsão. Isso acontece porque quando você estende os casos do modelo, os períodos usados para consultas de previsão sempre iniciam no término da série original. Portanto, se você adicionar dois novos pontos de dados, as duas primeiras previsões retornadas sobrepõem os novos dados.  
  
-   Depois que todos os novos pontos de dados forem usados, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fará previsões com base no modelo atualizado. Dessa forma, começando em setembro de 2005, você pode ver a diferença entre as previsões para M200 Europe a partir do modelo original, na coluna à esquerda, e a partir do modelo que usa EXTEND_MODEL_CASES, na coluna à direita. As previsões são diferentes porque o modelo foi atualizado com os novos dados.  
  
## <a name="using-start-and-end-time-steps-to-control-predictions"></a>Usando períodos inicial e final para controlar previsões  
 Quando você estende um modelo, os novos dados são sempre anexados ao fim da série. No entanto, para fins de previsão, as frações de tempo usadas para consultas de previsão sempre iniciam no término da série original. Se você quiser obter somente as previsões novas ao adicionar os novos dados, deverá especificar o ponto inicial como um número de frações de tempo. Por exemplo, se você estiver adicionando dois novos pontos de dados e quiser fazer quatro três previsões novas, proceda da seguinte forma:  
  
-   Crie uma PREDICTION JOIN em um modelo de série temporal e especifique dois meses de dados novos.  
  
-   Solicite previsões para quatro frações de tempo, onde o ponto inicial será 3 e o ponto final será a fração de tempo 6.  
  
 Em outras palavras, se seus novos dados contiverem n frações de tempo, e você solicitar previsões para períodos de 1 a n, as previsões coincidirão com o mesmo período dos dados novos. Para conseguir previsões para períodos de tempo não cobertos pelos seus dados, você deve iniciar as previsões na fração de tempo n+1 após a nova série de dados ou assegurar-se de solicitar frações de tempo adicionais.  
  
> [!NOTE]  
>  Não é possível fazer previsões históricas quando você adiciona novos dados.  
  
 O exemplo a seguir mostra a instrução DMX, que permite a você obter somente as novas previsões para as duas séries do exemplo anterior.  
  
```  
SELECT [Model Region],  
PredictTimeSeries([Quantity],3,6, EXTEND_MODEL_CASES) AS PredictQty  
FROM  
   [Forecasting_MIXED]  
NATURAL PREDICTION JOIN   
   SELECT 1 AS [ReportingDate],  
  '10' AS [Quantity],  
  'M200 Europe' AS [ModelRegion]  
UNION SELECT  
  2 AS [ReportingDate],  
  15 AS [Quantity]),  
  'M200 Europe' AS [ModelRegion]  
) AS t  
WHERE [ModelRegion] = 'M200 Europe'  
```  
  
 Os resultados da previsão começam na fração de tempo 3, que ocorre após os 2 meses de dados novos fornecidos por você.  
  
 **Produto e região: M200 Europa**  
  
 Modelo com dados atualizados (PredictTimeSeries com EXTEND_MODEL_CASES)  
  
||||  
|-|-|-|  
|M200 Europa|9/25/2008 12:00:00 AM|72|  
|M200 Europa|10/25/2008 12:00:00 AM|69|  
|M200 Europa|11/25/2008 12:00:00 AM|68|  
|M200 Europa|12/25/2008 12:00:00 AM|89|  
  
## <a name="making-predictions-with-replacemodelcases"></a>Fazendo previsões com REPLACE_MODEL_CASES  
 Substituir os casos de modelo é útil quando você desejar treinar um modelo em um conjunto de casos e, então, aplicar o modelo a uma série de dados diferente. Uma passo a passo detalhado desse cenário é apresentada na [lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de consulta de modelo de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
