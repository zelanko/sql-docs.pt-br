---
title: 'Lição 1: Criando um modelo de mineração e a estrutura de mineração de série temporal | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b201f2b8-9ab5-425b-9ff3-fe321a60a7b7
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0dc6f1be5fd1d0a6c983005d7db10c4c94a690b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251178"
---
# <a name="lesson-1-creating-a-time-series-mining-model-and-mining-structure"></a>Lição 1: Criando um modelo de mineração de série temporal e uma estrutura de mineração
  Nesta lição, você criará um modelo de mineração que permite prever valores com o passar do tempo, com base em dados históricos. Quando você criar o modelo, a estrutura subjacente será gerada automaticamente e poderá ser usada como a base para outros modelos de mineração.  
  
 Esta lição supõe que você já conhece modelos de previsão e os requisitos do algoritmo MTS. Para obter mais informações, consulte [Algoritmo MTS](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
## <a name="create-mining-model-statement"></a>Instrução CREATE MINING MODEL  
 Para criar um modelo de mineração diretamente e gerar automaticamente a estrutura de mineração subjacente, você deve usar o [CREATE MINING MODEL &#40;DMX&#41; ](/sql/dmx/create-mining-model-dmx) instrução. O código na instrução pode ser dividido nas seguintes partes:  
  
-   Nomeando o modelo  
  
-   Definindo o carimbo de data/hora  
  
-   Definindo coluna de chave da série opcional  
  
-   Definindo o atributo ou os atributos previsíveis  
  
 A seguir, um exemplo genérico da instrução CREATE MINING MODEL:  
  
```  
CREATE MINING MODEL [<Mining Structure Name>]  
(  
   <key columns>,  
   <predictable attribute columns>  
)  
USING <algorithm name>([parameter list])  
WITH DRILLTHROUGH  
```  
  
 A primeira linha do código define o nome do modelo de mineração:  
  
```  
CREATE MINING MODEL [Mining Model Name]  
```  
  
 O Analysis Services gera automaticamente um nome para a estrutura subjacente, ao anexar "_structure" ao nome do modelo, o que garante que o nome da estrutura seja diferente do nome do modelo. Para obter informações sobre como nomear um objeto no DMX, consulte [identificadores &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 A próxima linha do código define a coluna de chave do modelo de mineração que, no caso de um modelo de série temporal identifica exclusivamente um período na fonte de dados. A etapa temporal é identificada com as palavras-chave `KEY TIME` após o nome da coluna e os tipos de dados. Se o modelo de série temporal tiver uma chave de série separada, será identificado pela palavra-chave `KEY`.  
  
```  
<key columns>  
```  
  
 A próxima linha do código é usada para definir as colunas do modelo que serão previstas. Você pode ter vários atributos previsíveis em um único modelo de mineração. Quando há vários atributos previsíveis, o algoritmo MTS gera uma análise separada para cada série:  
  
```  
<predictable attribute columns>  
```  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Criar uma nova consulta em branco  
  
-   Alterar a consulta para criar o modelo de mineração  
  
-   Execute a consulta  
  
## <a name="creating-the-query"></a>Criando a consulta  
 A primeira etapa é se conectar a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e criar uma nova consulta DMX no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Para criar uma nova consulta DMX no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  No **conectar ao servidor** caixa de diálogo, para **tipo de servidor**, selecione **Analysis Services**. Na **nome do servidor**, digite `LocalHost`, ou o nome da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você deseja se conectar para esta lição. Clique em **Conectar**.  
  
3.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
## <a name="altering-the-query"></a>Alterando a consulta  
 A próxima etapa é modificar a instrução CREATE MINING MODEL para criar o modelo de mineração usado para previsão, junto com sua estrutura de mineração subjacente.  
  
#### <a name="to-customize-the-create-mining-model-statement"></a>Para personalizar a instrução CREATE MINING MODEL  
  
1.  No Editor de Consultas, copie o exemplo genérico da instrução CREATE MINING MODEL na consulta em branco.  
  
2.  Substitua o seguinte:  
  
    ```  
    [mining model name]   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
3.  Substitua o seguinte:  
  
    ```  
    <key columns>  
    ```  
  
     por:  
  
    ```  
    [Reporting Date] DATE KEY TIME,  
    [Model Region] TEXT KEY  
    ```  
  
     A palavra-chave `TIME KEY` indica que a coluna ReportingDate contém os valores de período usados na classificação dos valores. Períodos podem ser datas e horas, inteiros ou qualquer tipo de dados classificado, desde que os valores sejam exclusivos e que os dados estejam classificados.  
  
     As palavras-chave `TEXT` e `KEY` indicam que a coluna ModelRegion contém uma chave de série adicional. Você só pode ter uma chave de série e os valores da coluna devem ser distintos.  
  
4.  Substitua o seguinte:  
  
    ```  
    < predictable attribute columns> )  
    ```  
  
     por:  
  
    ```  
    [Quantity] LONG CONTINUOUS PREDICT,  
    [Amount] DOUBLE CONTINUOUS PREDICT  
    )  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    USING <algorithm name>([parameter list])  
    WITH DRILLTHROUGH  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Time_Series(AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
    ```  
  
     O parâmetro do algoritmo `AUTO_DETECT_PERIODICITY` = 0.8 indica que você deseja que o algoritmo detecte ciclos nos dados. Definir esse valor mais próximo a 1 favorece a descoberta de vários padrões mas pode diminuir a velocidade de processamento.  
  
     O parâmetro de algoritmo `FORECAST_METHOD` indica se você deseja que os dados sejam analisados usando ARTXP, ARIMA ou uma mistura de ambos.  
  
     A palavra-chave `WITH DRILLTHROUGH` especifica que você deseja ser capaz de exibir estatísticas detalhadas nos dados de origem após a conclusão do modelo. Adicione esta cláusula se quiser navegar pelos detalhes do modelo usando o Visualizador MTS. Ela não é obrigatória para a previsão.  
  
     A instrução completa agora deve ser:  
  
    ```  
    CREATE MINING MODEL [Forecasting_MIXED]  
         (  
        [Reporting Date] DATE KEY TIME,  
        [Model Region] TEXT KEY,  
        [Quantity] LONG CONTINUOUS PREDICT,  
        [Amount] DOUBLE CONTINUOUS PREDICT  
        )  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
  
    ```  
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Forecasting_MIXED.dmx`.  
  
## <a name="executing-the-query"></a>Executando a consulta  
 A última etapa é executar a consulta. Depois que você cria e salva a consulta, ela deve ser executada para criar o modelo de mineração e sua estrutura de mineração no servidor. Para obter mais informações sobre como executar consultas no Editor de consultas, consulte [Editor de consultas do mecanismo de banco de dados &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Para executar a consulta.  
  
-   No Editor de consultas, na barra de ferramentas, clique em **Execute**.  
  
     O status da consulta é exibido na **mensagens** guia na parte inferior do Editor de consultas após a instrução termina a execução. As mensagens devem exibir:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Uma estrutura nova nomeada **Forecasting_MIXED_Structure** agora existe no servidor, junto com o modelo de mineração relacionado **Forecasting_MIXED**.  
  
 Na próxima lição, você adicionará um modelo de mineração para o **Forecasting_MIXED** estrutura de mineração que você acabou de criar.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Adicionando modelos de mineração à estrutura de mineração de série temporal](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
  
## <a name="see-also"></a>Consulte também  
 [Mining Model Content para modelos de série temporal &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)   
 [Referência técnica do algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
