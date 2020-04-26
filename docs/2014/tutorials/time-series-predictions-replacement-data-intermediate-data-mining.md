---
title: Previsões de série temporal usando dados de substituição (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c96b70775105ea9446810ac3b064ae7cb07d4337
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312875"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>Previsões de série temporal usando dados de substituição (Tutorial de mineração de dados intermediário)
  Nesta tarefa, você criará um novo modelo com base em dados de vendas mundiais. Depois, você criará uma consulta de previsão que aplica o modelo de vendas mundial a uma das regiões individuais.  
  
## <a name="building-a-general-model"></a>Criando um modelo geral  
 Lembre-se de que sua análise dos resultados do modelo de mineração original revelaram grandes diferenças entre as regiões e as linhas de produtos. Por exemplo, as vendas na América do Norte eram fortes para o modelo M200, enquanto que as vendas do modelo de T1000 não iam tão bem. No entanto, a análise é complicada pelo fato de que algumas séries não tinham muitos dados ou dados iniciados em um ponto diferente no tempo. Alguns dados também estavam faltando.  
  
 ![Séries que preveem a quantidade M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "Séries que preveem a quantidade M200 e T1000")  
  
 Para solucionar alguns dos problemas de qualidade de dados, você decide mesclar os dados de vendas do mundo todo e usar esse conjunto de tendências geral de vendas para criar um modelo que possa ser aplicado à previsão de vendas futuras em qualquer região.  
  
 Quando você for criar as previsões, usará o padrão gerado pelo treinamento sobre dados de vendas mundiais, mas substituirá os pontos de dados históricos pelos dados de vendas de cada região. Dessa maneira, a forma da tendência é preservada mas os valores previstos ficam alinhados com os números de vendas históricos de cada região e modelo.  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>Fazendo uma previsão cruzada com um modelo de série temporal  
 O processo de usar dados de uma série para prever tendências em outra série é chamado previsão cruzada. Você pode usar a previsão cruzada em muitos cenários: por exemplo, você poderia decidir que vendas de televisão são uma profeta boa de atividade econômica global, e aplicar um modelo treinou vendas na televisão a dados econômicos gerais.  
  
 No SQL Server mineração de dados, você executa a previsão cruzada usando o parâmetro REPLACE_MODEL_CASES dentro dos argumentos para a função, [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
 Na próxima tarefa, você aprenderá a usar REPLACE_MODEL_CASES. Você usará os dados de vendas mundiais mesclados para criar um modelo e depois criará uma consulta de previsão que mapeia o modelo geral nos dados de substituição.  
  
 Estamos partindo do princípio de que você está familiarizado com o método de criação de modelos de mineração de dados agora e, portanto, as instruções para criar o modelo foram simplificadas.  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>Para criar uma estrutura de mineração e um modelo de mineração usando os dados agregados  
  
1.  Em **Gerenciador de soluções**, clique com o botão direito do mouse em **estruturas de mineração**e selecione **nova estrutura de mineração** para iniciar o assistente de mineração de dados.  
  
2.  No Assistente de Mineração de Dados, faça as seguintes seleções:  
  
    -   Algoritmo: Microsoft Time Series  
  
    -   Use a fonte de dados que você criou anteriormente nesta lição avançada como a origem do modelo. Consulte [&#41;de previsões de série temporal avançada &#40;tutorial de mineração de dados intermediário ](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md).  
  
         Exibição da fonte de dados:`AllRegions`  
  
    -   Escolha as seguintes colunas para a chave de série e chave de tempo:  
  
         Hora da chave: ReportingDate  
  
         Chave: região  
  
    -   Escolha as seguintes colunas para `Input` e `Predict`:  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   Para **nome da estrutura de mineração**, digite:`All Regions`  
  
    -   Para **nome do modelo de mineração**, digite:`All Regions`  
  
3.  Processe a nova estrutura e o novo modelo.  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>Para criar a consulta de previsão e mapear os dados de substituição  
  
1.  Se o modelo ainda não estiver aberto, clique duas vezes na estrutura de regiões e, no designer de mineração de dados, clique na guia **previsão do modelo de mineração** .  
  
2.  No painel **modelo de mineração** , as regiões do modelo já devem estar selecionadas. Se não estiver selecionado, clique em **selecionar modelo**e, em seguida, selecione o modelo, regiões.  
  
3.  No painel **selecionar tabela (s) de entrada** , clique em **selecionar tabela de casos**.  
  
4.  Na caixa de diálogo **selecionar tabela** , altere a fonte de dados para T1000 região do Pacífico e clique em **OK**.  
  
5.  Clique com o botão direito do mouse na linha de junção entre o modelo de mineração e os dados de entrada e selecione **Modificar Conexões**. Mapeie os dados na exibição da fonte de dados do modelo como segue:  
  
    1.  Verifique se a coluna ReportingDate no modelo de mineração está mapeada para a coluna ReportingDate nos dados de entrada.  
  
    2.  Na caixa de diálogo **modificar mapeamento** , na linha da coluna de modelo AvgQty, clique em **coluna de tabela** e selecione T1000 Pacífico. quantity. Clique em **OK**.  
  
         Esta etapa mapeia a coluna que você criou no modelo para prever a quantidade média para os dados reais da série T1000 em relação à quantidade de vendas.  
  
    3.  Não mapeie a região da coluna no modelo para qualquer coluna de entrada.  
  
         Como o modelo agregou os dados em todas as séries, não há nenhuma correspondência para os valores de séries como T1000 Pacífico e um erro é gerado quando as consultas de previsão são executadas.  
  
6.  Agora você criará a consulta de previsão.  
  
     Primeiramente, adicione uma coluna aos resultados gerados em AllRegions do modelo junto com as previsões. Desse modo, você saberá que os resultados foram baseados no modelo geral.  
  
    1.  Na grade, clique na primeira linha vazia, em **origem**, e selecione modelo de mineração das regiões.  
  
    2.  Para **campo**, selecione região.  
  
    3.  Para **alias**, digite o **modelo usado**.  
  
7.  Em seguida, adicione um rótulo aos resultados para que seja possível ver a que série a previsão se destina.  
  
    1.  Clique em uma linha vazia e, em **origem**, selecione **expressão personalizada**.  
  
    2.  Na coluna **alias** , digite **ModelRegion**.  
  
    3.  Na coluna **critérios/argumento** , digite `'T1000 Pacific'`.  
  
8.  Agora você configurará a função da previsão cruzada.  
  
    1.  Clique em uma linha vazia e, em **origem**, selecione **função de previsão**.  
  
    2.  Na coluna **campo** , selecione **PredictTimeSeries**.  
  
    3.  Para **alias**, digite **valores previstos**.  
  
    4.  Arraste o campo AvgQty do painel **modelo de mineração** para a coluna **critérios/argumento** usando a operação de arrastar e soltar.  
  
    5.  Na coluna **critérios/argumento** , após o nome do campo, digite o seguinte texto:`,5, REPLACE_MODEL_CASES`  
  
         O texto completo da caixa de texto **critérios/argumento** deve ser o seguinte:`[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. Clique em **resultados**.  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>Criando a consulta da previsão cruzada em DMX  
 Você deve ter notado um problema com a previsão cruzada: isto é, para aplicar o modelo geral a uma série de dados diferente, como o modelo de produto T1000 na região de América do Norte, você deve criar uma consulta diferente para cada série, de forma que você possa mapear cada conjunto de entradas para o modelo.  
  
 Porém, em vez de criar a consulta no designer, você pode mudar para exibição DMX e editar a instrução DMX que você criou. Por exemplo, a seguinte instrução DMX representa a consulta recém-criada:  
  
```  
SELECT  
      ([All Regions].[Region]) as [Model Used],  
      ('T-1000 Pacific') as [ModelRegion],  
      (PredictTimeSeries([All Regions].[Avg Qty],5, REPLACE_MODEL_CASES)) as [Predicted Quantity]  
     FROM [All Regions]  
PREDICTION JOIN  
    OPENQUERY([Adventure Works DW2003R2], 'SELECT [ReportingDate] FROM  
      (  
       SELECT  ReportingDate, ModelRegion, Quantity, Amount   
       FROM dbo.vTimeSeries   
       WHERE (ModelRegion = N''T1000 Pacific'')  
       ) as [T1000 Pacific]    ')   
    AS t  
ON   
[All Regions].[Reporting Date] = t.[ReportingDate]   
AND   
[All Regions].[Avg Qty] = t.[Quantity]  
```  
  
 Para aplicá-la a um modelo diferente, basta editar a instrução da consulta para substituir a condição do filtro e atualizar os rótulos associados a cada resultado.  
  
 Por exemplo, se você alterar as condições do filtro e os rótulos de coluna substituindo 'Pacífico' por 'América do Norte', obterá previsões para o produto T1000 na América do Norte, com base nos padrões do modelo geral.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Comparando previsões para modelos de previsão &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de consulta de modelo de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
