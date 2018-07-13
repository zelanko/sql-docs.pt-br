---
title: Usando dados atualizados (Tutorial mineração de dados intermediário) de previsões de série temporal | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8739f9be1ad015471017d17947ece1586663959b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278304"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>Previsões de série temporal usando dados atualizados (Tutorial de mineração de dados intermediário)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>Criando previsões usando os dados de vendas estendidos  
 Nesta lição, você criará uma consulta de previsão que adiciona os novos dados de vendas ao modelo. Ao estender o modelo com novos dados, você poderá obter previsões atualizadas que incluem os pontos de dados mais recentes.  
  
 É fácil criar previsões de série temporal que usam novos dados: basta adicionar o parâmetro EXTEND_MODEL_CASES para o [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) funcionar, especificar a origem dos novos dados e especificar quantos previsões que você deseja obter.  
  
> [!WARNING]  
>  O parâmetro EXTEND_MODEL_CASES é opcional; por padrão, o modelo é estendido a qualquer momento que você cria uma consulta de previsão de série temporal unindo novos dados como entradas.  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>Para criar a consulta de previsão e adicionar novos dados  
  
1.  Se o modelo não ainda estiver aberto, clique duas vezes a estrutura previsão e no Designer de mineração de dados, clique o **previsão de modelo de mineração** guia.  
  
2.  No **modelo de mineração** painel, o modelo de previsão já deve estar selecionado. Se não for selecionada, clique em **Selecionar modelo**e, em seguida, selecione o modelo Forecasting.  
  
3.  No **Selecionar tabela (s) de entrada** painel, clique em **Selecionar tabela de casos**.  
  
4.  No **Selecionar tabela** caixa de diálogo, selecione a fonte de dados, [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)].  
  
     Na lista de exibições da fonte de dados, selecione NewSalesData e, em seguida, clique em **Okey**.  
  
5.  A superfície da área de design com o botão direito e selecione **modificar conexões**.  
  
6.  Usando o **modificar mapeamento** caixa de diálogo caixa, mapear as colunas no modelo para as colunas nos dados externos, da seguinte maneira:  
  
    -   Mapear a coluna ReportingDate no modelo de mineração para a coluna de NewDate nos dados de entrada.  
  
    -   Mapear a coluna de valor no modelo de mineração para a coluna de NewAmount nos dados de entrada.  
  
    -   Mapear a coluna de quantidade no modelo de mineração para a coluna NewQty nos dados de entrada.  
  
    -   Mapear a coluna ModelRegion no modelo de mineração para a coluna de série nos dados de entrada.  
  
7.  Agora você criará a consulta de previsão.  
  
     Primeiramente, adicione uma coluna à consulta de previsão para produzir a série à qual a previsão se aplica.  
  
    1.  Na grade, clique na primeira linha vazia, sob **origem**e, em seguida, selecione a previsão.  
  
    2.  No **campo** coluna, selecione modelo de região e para **Alias**, tipo `Model Region`.  
  
8.  Em seguida, adicione e edite a função de previsão.  
  
    1.  Clique em uma linha vazia e, em **fonte**, selecione **função de previsão**.  
  
    2.  Para **campo**, selecione **PredictTimeSeries**.  
  
    3.  Para **Alias**, digite **valores previstos**.  
  
    4.  Arraste o campo Quantidade do **modelo de mineração** painel para o **critérios/argumento** coluna.  
  
    5.  No **critérios/argumento** coluna, após o nome do campo, digite o seguinte texto: **5,extend_model_cases**  
  
         O texto completo do **critérios/argumento** caixa de texto deve ser da seguinte maneira: `[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. Clique em **resultados** e examine os resultados.  
  
     As previsões começam em julho (o primeiro intervalo de tempo após o término dos dados originais) e terminam em novembro (o quinto intervalo de tempo após o término dos dados originais).  
  
 Você pode ver que para usar este tipo de consulta de previsão efetivamente, é preciso saber quando os dados antigos terminam, bem como quantos intervalos de tempo há nos novos dados.  
  
 Por exemplo, neste modelo, a série de dados original terminava em junho, e os dados para os meses de julho, agosto e setembro.  
  
 As previsões que usam EXTEND_MODEL_CASES sempre começam ao término da série de dados original. Portanto, se você desejar obter somente as previsões para os meses desconhecidos, deverá especificar os pontos de início e término para a previsão. Ambos os valores são especificados como vários intervalos de tempo que iniciam ao término dos dados antigos.  
  
 O procedimento a seguir demonstra como fazer isso.  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>Alterar os pontos de início e término das previsões  
  
1.  No construtor de consultas de previsão, clique em **consulta** para alternar para a exibição DMX.  
  
2.  Localize a instrução DMX que contém a função PredictTimeSeries e altere-a como segue:  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  Clique em **resultados** e examine os resultados.  
  
     Agora as previsões começam em outubro (o quarto intervalo de tempo, contando do término dos dados originais) e terminam em dezembro (o sexto intervalo de tempo, contando do término dos dados originais).  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Usando dados de substituição de previsões de série temporal &#40;Tutorial intermediário de mineração de dados&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica do algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Mining Model Content para modelos de série temporal &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
