---
title: 'Lição 4: Criando previsões de série temporal usando DMX | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6b883e43-209d-489a-8dc3-9349f88acae8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 772e5f5f71ca82dd18fec48730522c80e907414f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312087"
---
# <a name="lesson-4-creating-time-series-predictions-using-dmx"></a>Lição 4: Como criar previsões de série temporal usando DMX
  Esta lição e a próxima lição, você irá usar extensões DMX (Data Mining) para criar tipos diferentes de previsões com base em modelos de série temporal que você criou na [lição 1: Criando um modelo de mineração e a estrutura de mineração de série temporal](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md) e [lição 2: Adicionando modelos de mineração para a estrutura de mineração de série temporal](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md).  
  
 Com um modelo de série temporal, você tem várias opções para fazer previsões:  
  
-   Usar os padrões e os dados existentes no modelo de mineração  
  
-   Usar os padrões existentes no modelo de mineração mas fornecer dados novos  
  
-   Adicionar novos dados ao modelo ou atualizá-lo.  
  
 A sintaxe para criar esses tipos de previsão foi resumida a seguir:  
  
 Previsão de série temporal padrão  
 Use [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) para retornar o número especificado de previsões do modelo de mineração treinado.  
  
 Por exemplo, consulte [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) ou [exemplos de consulta de modelo de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md).  
  
 EXTEND_MODEL_CASES  
 Use [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) com o argumento EXTEND_MODEL_CASES para adicionar novos dados, a série de estender e criar previsões com base no modelo de mineração atualizado.  
  
 Este tutorial contém um exemplo de como usar EXTEND_MODEL_CASES.  
  
 REPLACE_MODEL_CASES  
 Use [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) com o argumento REPLACE_MODEL_CASES para substituir os dados originais por uma nova série de dados e, em seguida, criar previsões com base na aplicação dos padrões no modelo de mineração para os novos dados série.  
  
 Para obter um exemplo de como usar REPLACE_MODEL_CASES, consulte [lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Criar uma consulta para obter as previsões padrão com base em dados existentes.  
  
 Na lição a seguir, você executará as seguintes tarefas relacionadas:  
  
-   Criar uma consulta para fornecer novos dados e obter previsões atualizadas.  
  
 Além de criar consultas manualmente usando DMX, você também pode criar previsões usando o construtor de consultas de previsão no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="simple-time-series-prediction-query"></a>Consulta de previsão de série temporal simples  
 A primeira etapa é usar a instrução `SELECT FROM` junto com a função `PredictTimeSeries` para criar previsões de série temporal. Modelos de série temporal dão suporte a uma sintaxe simplificada para a criação de previsões: você não precisa fornecer qualquer entrada, mas especificar o número de previsões a serem criadas. A seguir, um exemplo genérico da instrução que será usada:  
  
```  
SELECT <select list>   
FROM [<mining model name>]   
WHERE [<criteria>]  
```  
  
 A lista de seleção pode conter colunas do modelo, como o nome do produto da linha que você está criando as previsões, ou funções de previsão, como [Lag &#40;DMX&#41; ](/sql/dmx/lag-dmx) ou [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx), que são especificamente para modelos de mineração de série temporal.  
  
#### <a name="to-create-a-simple-time-series-prediction-query"></a>Para criar uma consulta de previsão de série temporal simples  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    ```  
  
     A primeira linha recupera um valor do modelo de mineração que identifica a série.  
  
     A segunda e a terceira linhas usam a função `PredictTimeSeries`. Cada linha prevê um atributo diferente, `[Quantity]` ou `[Amount]`. Os números depois dos nomes dos atributos previsíveis especificam o número de períodos a serem previstos.  
  
     A cláusula `AS` é usada para fornecer um nome para a coluna retornada por cada função de previsão. Se você não fornecer um alias, por padrão ambas as colunas serão retornadas com o rótulo `Expression`.  
  
4.  Substitua o seguinte:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    WHERE [criteria>]   
    ```  
  
     por:  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    FROM   
    [Forecasting_MIXED]  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `SimpleTimeSeriesPrediction.dmx`.  
  
8.  Na barra de ferramentas, clique o **Execute** botão.  
  
     A consulta retorna 6 previsões para cada uma das duas combinações de produto e região especificadas na cláusula `WHERE`.  
  
 Na próxima lição, você criará uma consulta para fornecer novos dados ao modelo e comparar os resultados da previsão aos da previsão recém-criada.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Lição 5: Estendendo a série temporal de modelo](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
  
## <a name="see-also"></a>Consulte também  
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)   
 [Lag &#40;DMX&#41;](/sql/dmx/lag-dmx)   
 [Exemplos de consulta de modelo de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
  
