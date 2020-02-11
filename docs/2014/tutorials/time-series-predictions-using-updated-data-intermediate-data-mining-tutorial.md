---
title: Previsões de série temporal usando dados atualizados (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2017defaba74071b1a12bee14a5d8907e4c71cda
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067552"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>Previsões de série temporal usando dados atualizados (Tutorial de mineração de dados intermediário)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>Criando previsões usando os dados de vendas estendidos  
 Nesta lição, você criará uma consulta de previsão que adiciona os novos dados de vendas ao modelo. Ao estender o modelo com novos dados, você poderá obter previsões atualizadas que incluem os pontos de dados mais recentes.  
  
 Criar previsões de série temporal que usam novos dados é fácil: basta adicionar o parâmetro EXTEND_MODEL_CASES à função de [&#41;PredictTimeSeries &#40;DMX](/sql/dmx/predicttimeseries-dmx) , especificar a origem dos novos dados e especificar quantas previsões você deseja obter.  
  
> [!WARNING]  
>  O parâmetro EXTEND_MODEL_CASES é opcional; por padrão, o modelo é estendido a qualquer momento que você cria uma consulta de previsão de série temporal unindo novos dados como entradas.  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>Para criar a consulta de previsão e adicionar novos dados  
  
1.  Se o modelo ainda não estiver aberto, clique duas vezes na estrutura de previsão e, no designer de mineração de dados, clique na guia **previsão do modelo de mineração** .  
  
2.  No painel **modelo de mineração** , a previsão do modelo já deve estar selecionada. Se não estiver selecionado, clique em **selecionar modelo**e, em seguida, selecione o modelo, previsão.  
  
3.  No painel **selecionar tabela (s) de entrada** , clique em **selecionar tabela de casos**.  
  
4.  Na caixa de diálogo **selecionar tabela** , selecione a fonte de dados [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)],.  
  
     Na lista de exibições da fonte de dados, selecione NewSalesData e clique em **OK**.  
  
5.  Clique com o botão direito do mouse na superfície da área de design e selecione **Modificar Conexões**.  
  
6.  Usando a caixa de diálogo **modificar mapeamento** , mapeie as colunas no modelo para as colunas nos dados externos da seguinte maneira:  
  
    -   Mapeie a coluna ReportingDate no modelo de mineração para a coluna NewDate nos dados de entrada.  
  
    -   Mapeie a coluna de valor no modelo de mineração para a coluna NewAmount nos dados de entrada.  
  
    -   Mapeie a coluna quantidade no modelo de mineração para a coluna NewQty nos dados de entrada.  
  
    -   Mapeie a coluna ModelRegion no modelo de mineração para a coluna série nos dados de entrada.  
  
7.  Agora você criará a consulta de previsão.  
  
     Primeiramente, adicione uma coluna à consulta de previsão para produzir a série à qual a previsão se aplica.  
  
    1.  Na grade, clique na primeira linha vazia, em **origem**, e selecione previsão.  
  
    2.  Na coluna **campo** , selecione região do modelo e para **alias**, digite `Model Region`.  
  
8.  Em seguida, adicione e edite a função de previsão.  
  
    1.  Clique em uma linha vazia e, em **origem**, selecione **função de previsão**.  
  
    2.  Para **campo**, selecione **PredictTimeSeries**.  
  
    3.  Para **alias**, digite **valores previstos**.  
  
    4.  Arraste a quantidade de campo do painel **modelo de mineração** até a coluna **critérios/argumento** .  
  
    5.  Na coluna **critérios/argumento** , após o nome do campo, digite o seguinte texto: **5, EXTEND_MODEL_CASES**  
  
         O texto completo da caixa de texto **critérios/argumento** deve ser o seguinte:`[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. Clique em **resultados** e examine os resultados.  
  
     As previsões começam em julho (o primeiro intervalo de tempo após o término dos dados originais) e terminam em novembro (o quinto intervalo de tempo após o término dos dados originais).  
  
 Você pode ver que para usar este tipo de consulta de previsão efetivamente, é preciso saber quando os dados antigos terminam, bem como quantos intervalos de tempo há nos novos dados.  
  
 Por exemplo, neste modelo, a série de dados original terminava em junho, e os dados para os meses de julho, agosto e setembro.  
  
 As previsões que usam EXTEND_MODEL_CASES sempre começam ao término da série de dados original. Portanto, se você desejar obter somente as previsões para os meses desconhecidos, deverá especificar os pontos de início e término para a previsão. Ambos os valores são especificados como vários intervalos de tempo que iniciam ao término dos dados antigos.  
  
 O procedimento a seguir demonstra como fazer isso.  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>Alterar os pontos de início e término das previsões  
  
1.  Em previsão Construtor de Consultas, clique em **consulta** para alternar para a exibição DMX.  
  
2.  Localize a instrução DMX que contém a função PredictTimeSeries e altere-a como segue:  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  Clique em **resultados** e examine os resultados.  
  
     Agora as previsões começam em outubro (o quarto intervalo de tempo, contando do término dos dados originais) e terminam em dezembro (o sexto intervalo de tempo, contando do término dos dados originais).  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Previsões de série temporal usando dados de substituição &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica do algoritmo do Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de série temporal &#40;mineração de dados Analysis Services&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
