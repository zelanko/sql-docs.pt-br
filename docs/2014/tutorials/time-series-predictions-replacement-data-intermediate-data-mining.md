---
title: Usando dados de substituição (Tutorial mineração de dados intermediário) de previsões de série temporal | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010228"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>Previsões de série temporal usando dados de substituição (Tutorial de mineração de dados intermediário)
  Nesta tarefa, você criará um novo modelo com base em dados de vendas mundiais. Depois, você criará uma consulta de previsão que aplica o modelo de vendas mundial a uma das regiões individuais.  
  
## <a name="building-a-general-model"></a>Criando um modelo geral  
 Lembre-se de que sua análise dos resultados do modelo de mineração original revelaram grandes diferenças entre as regiões e as linhas de produtos. Por exemplo, as vendas na América do Norte eram fortes para o modelo M200, enquanto que as vendas do modelo de T1000 não iam tão bem. No entanto, a análise é complicada pelo fato de que algumas séries não tinham muitos dados ou dados iniciavam em um ponto diferente no tempo. Alguns dados também estavam faltando.  
  
 ![Séries que preveem a quantidade M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "séries que preveem a quantidade M200 e T1000")  
  
 Para solucionar alguns dos problemas de qualidade de dados, você decide mesclar os dados de vendas do mundo todo e usar esse conjunto de tendências geral de vendas para criar um modelo que possa ser aplicado à previsão de vendas futuras em qualquer região.  
  
 Quando você for criar as previsões, usará o padrão gerado pelo treinamento sobre dados de vendas mundiais, mas substituirá os pontos de dados históricos pelos dados de vendas de cada região. Dessa maneira, a forma da tendência é preservada mas os valores previstos ficam alinhados com os números de vendas históricos de cada região e modelo.  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>Fazendo uma previsão cruzada com um modelo de série temporal  
 O processo de usar dados de uma série para prever tendências em outra série é chamado previsão cruzada. Você pode usar a previsão cruzada em muitos cenários: por exemplo, você poderia decidir que vendas de televisão são uma profeta boa de atividade econômica global, e aplicar um modelo treinou vendas na televisão a dados econômicos gerais.  
  
 No SQL Server Data Mining, você deve executar previsão cruzada, usando o parâmetro REPLACE_MODEL_CASES nos argumentos para a função [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
 Na próxima tarefa, você aprenderá a usar REPLACE_MODEL_CASES. Você usará os dados de vendas mundiais mesclados para criar um modelo e depois criará uma consulta de previsão que mapeia o modelo geral nos dados de substituição.  
  
 Estamos partindo do princípio de que você está familiarizado com o método de criação de modelos de mineração de dados agora e, portanto, as instruções para criar o modelo foram simplificadas.  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>Para criar uma estrutura de mineração e um modelo de mineração usando os dados agregados  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **estruturas de mineração**e, em seguida, selecione **nova estrutura de mineração** para iniciar o Assistente de mineração de dados.  
  
2.  No Assistente de Mineração de Dados, faça as seguintes seleções:  
  
    -   Algoritmo: Microsoft Time Series  
  
    -   Use a fonte de dados que você criou anteriormente nesta lição avançada como a origem do modelo. Ver [avançadas de previsões de série temporal &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md).  
  
         Exibição de fonte de dados: `AllRegions`  
  
    -   Escolha as seguintes colunas para a chave de série e chave de tempo:  
  
         Tempo-chave: ReportingDate  
  
         Chave: Região  
  
    -   Escolha as seguintes colunas para `Input` e `Predict`:  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   Para **nome da estrutura de mineração**, tipo: `All Regions`  
  
    -   Para **nome do modelo de mineração**, tipo: `All Regions`  
  
3.  Processe a nova estrutura e o novo modelo.  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>Para criar a consulta de previsão e mapear os dados de substituição  
  
1.  Se o modelo não ainda estiver aberto, clique duas vezes na estrutura Allregios e no Designer de mineração de dados, clique o **previsão de modelo de mineração** guia.  
  
2.  No **modelo de mineração** painel, o modelo AllRegions já deve estar selecionado. Se não for selecionada, clique em **Selecionar modelo**e, em seguida, selecione o modelo, AllRegions.  
  
3.  No **Selecionar tabela (s) de entrada** painel, clique em **Selecionar tabela de casos**.  
  
4.  No **Selecionar tabela** caixa de diálogo, altere os dados de origem para T1000 Pacific Region e, em seguida, clique em **Okey**.  
  
5.  Clique com botão direito na linha de junção entre o modelo de mineração e os dados de entrada e selecione **modificar conexões**. Mapeie os dados na exibição da fonte de dados do modelo como segue:  
  
    1.  Verifique se a coluna ReportingDate no modelo de mineração é mapeada para a coluna ReportingDate nos dados de entrada.  
  
    2.  No **modificar mapeamento** caixa de diálogo, na linha para a coluna do modelo AvgQty, clique em **coluna da tabela** e, em seguida, selecione T1000 Pacific. Clique em **OK**.  
  
         Esta etapa mapeia a coluna que você criou no modelo para prever a quantidade média para os dados reais da série T1000 em relação à quantidade de vendas.  
  
    3.  Não mapeie a coluna de região no modelo para qualquer coluna de entrada.  
  
         Como o modelo agregou os dados em todas as séries, não há nenhuma correspondência para os valores de séries como T1000 Pacífico e um erro é gerado quando as consultas de previsão são executadas.  
  
6.  Agora você criará a consulta de previsão.  
  
     Primeiramente, adicione uma coluna aos resultados gerados em AllRegions do modelo junto com as previsões. Desse modo, você saberá que os resultados foram baseados no modelo geral.  
  
    1.  Na grade, clique na primeira linha vazia, sob **origem**e, em seguida, selecione o modelo de mineração AllRegions.  
  
    2.  Para **campo**, selecione a região.  
  
    3.  Para **Alias**, digite **modelo usado**.  
  
7.  Em seguida, adicione um rótulo aos resultados para que seja possível ver a que série a previsão se destina.  
  
    1.  Clique em uma linha vazia e, em **fonte**, selecione **expressão personalizada**.  
  
    2.  No **Alias** coluna, digite **ModelRegion**.  
  
    3.  No **critérios/argumento** coluna, digite `'T1000 Pacific'`.  
  
8.  Agora você configurará a função da previsão cruzada.  
  
    1.  Clique em uma linha vazia e, em **fonte**, selecione **função de previsão**.  
  
    2.  No **campo** coluna, selecione **PredictTimeSeries**.  
  
    3.  Para **Alias**, digite **valores previstos**.  
  
    4.  Arraste o campo AvgQty do **modelo de mineração** painel para o **critérios/argumento** coluna usando a operação de arrastar e soltar.  
  
    5.  No **critérios/argumento** coluna, após o nome do campo, digite o seguinte texto: `,5, REPLACE_MODEL_CASES`  
  
         O texto completo do **critérios/argumento** caixa de texto deve ser da seguinte maneira: `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
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
 [Comparando previsões para modelos de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de consulta de modelo de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
