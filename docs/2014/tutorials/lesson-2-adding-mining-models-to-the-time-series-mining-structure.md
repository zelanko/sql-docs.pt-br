---
title: 'Lição 2: adicionando modelos de mineração à estrutura de mineração de série temporal | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ae0bb91fafb53c0c077a4e0d82558b550d0e6070
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62855713"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>Lição 2: Adicionando modelos de mineração à estrutura de mineração de série temporal
  Nesta lição, você adicionará um novo modelo de mineração à estrutura de mineração que acabou de criar na [lição 1: Criando um modelo de mineração de série temporal e estrutura de mineração](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md).  
  
## <a name="alter-mining-structure-statement"></a>Instrução ALTER MINING STRUCTURE  
 Para adicionar um novo modelo de mineração a uma estrutura de mineração existente, use a instrução [ALTER MINING structure &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) . O código na instrução pode ser dividido nas seguintes partes:  
  
-   Identificando a estrutura de mineração  
  
-   Nomeando o modelo de mineração  
  
-   Definindo a coluna de chave  
  
-   Definindo as colunas previsíveis  
  
-   Especificando as alterações de algoritmo e de qualquer parâmetro  
  
 A seguir, veja um exemplo genérico da instrução ALTER MINING STRUCTURE:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
   ([<key columns>],  
    <mining model columns>  
   )  
USING <algorithm name>([<algorithm parameters>])  
[WITH DRILLTHROUGH]  
```  
  
 A primeira linha do código identifica a estrutura de mineração existente à qual os modelos de mineração serão adicionados:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 A linha seguinte do código nomeia o modelo de mineração que será adicionado à estrutura de mineração:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Para obter informações sobre como nomear um objeto no DMX, consulte [identificadores &#40;&#41;DMX ](/sql/dmx/identifiers-dmx).  
  
 As linhas seguintes do código definem as colunas a partir da estrutura de mineração que será usada pelo modelo de mineração:  
  
```  
[<key columns>],  
<mining model columns>  
```  
  
 Você só pode usar colunas que já existem na estrutura de mineração, e a primeira coluna na lista deve ser a coluna de chave da estrutura de mineração.  
  
 A próximas linhas do código definem o algoritmo de mineração que gera o modelo de mineração e os parâmetros que podem ser definidos no algoritmo, além de especificarem se você pode detalhar a partir do modelo de mineração até a exibição de dados nos casos de treinamento:  
  
```  
USING <algorithm name>([<algorithm parameters>])  
WITH DRILLTHROUGH  
```  
  
 Para obter mais informações sobre os parâmetros de algoritmo que você pode ajustar, consulte [referência técnica do algoritmo do Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Você pode especificar que uma coluna no modelo de mineração seja utilizada para previsão usando a seguinte sintaxe:  
  
```  
<mining model column> PREDICT  
```  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Adicionar um novo modelo de mineração de série temporal à estrutura.  
  
-   Alterar os parâmetros do algoritmo para usar um método de análise e uma previsão diferentes  
  
## <a name="adding-an-arima-time-series-model-to-the-structure"></a>Adicionar um modelo de série temporal ARIMA à estrutura  
 A primeira etapa é adicionar um novo modelo de mineração de previsão à estrutura existente. Por padrão, o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Times Series cria modelos de mineração de série temporal usando dois algoritmos, ARIMA e ARTXP, combinando os resultados. No entanto, você pode especificar um único algoritmo para usar ou pode especificar a combinação exata de algoritmos. Nesta etapa, você adicionará um novo modelo que só utiliza o algoritmo ARIMA. Este algoritmo foi otimizado para previsão de longo prazo.  
  
#### <a name="to-add-an-arima-time-series-mining-model"></a>Para adicionar um modelo de mineração de série temporal ARIMA  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX** para abrir o editor de consultas e uma nova consulta em branco.  
  
2.  Copie o exemplo genérico da instrução ALTER MINING STRUCTURE na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED_Structure]  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    Forecasting_ARIMA  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    <key columns>,  
    ```  
  
     por:  
  
    ```  
    [ReportingDate],  
    [ModelRegion]  
    ```  
  
     Observe que não é preciso repetir as informações de tipo de data ou de tipo de conteúdo fornecidas na instrução CREATE MINING MODEL, uma vez que elas já estão armazenadas na estrutura de mineração.  
  
6.  Substitua o seguinte:  
  
    ```  
    <mining model columns>  
    ```  
  
     por:  
  
    ```  
    ([Quantity] PREDICT,  
    [Amount] PREDICT  
    )  
    ```  
  
7.  Substitua o seguinte:  
  
    ```  
    USING <algorithm name>([<algorithm parameters>])   
    [WITH DRILLTHROUGH]  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
     A instrução resultante deverá ser agora:  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARIMA]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
8.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
9. Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Forecasting_ARIMA.dmx`.  
  
10. Na barra de ferramentas, clique no botão **executar** .  
  
## <a name="adding-an-artxp-time-series-model-to-the-structure"></a>Adicionar um modelo de série temporal ARTXP à estrutura  
 O algoritmo ARTXP era o algoritmo padrão de série temporal do SQL Server 2005 e é otimizado para previsões a curto prazo. Para comparar previsões usando todos os três algoritmos de série temporal, você adicionará mais um modelo, baseado no algoritmo ARTXP.  
  
#### <a name="to-add-an-artxp-time-series-mining-model"></a>Para adicionar um modelo de mineração de série temporal ARTXP  
  
1.  Copie o código a seguir em uma janela de consulta em branco.  
  
     Observe que não é necessário alterar nada, exceto o nome do novo modelo de mineração e o valor do parâmetro FORECAST_METHOD.  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARTXP]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARTXP')  
    WITH DRILLTHROUGH  
    ```  
  
2.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
3.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Forecasting_ARTXP.dmx`.  
  
4.  Na barra de ferramentas, clique no botão **executar** .  
  
 Na próxima lição, você processará todos os modelos e a estrutura de mineração.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 3: Processando a estrutura e os modelos de série temporal](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo do Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Referência técnica do algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
