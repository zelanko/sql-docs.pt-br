---
title: Funções de previsão gerais (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6db4adccfa0786e2acb1ce45725758d6b302b51f
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363016"
---
# <a name="general-prediction-functions-dmx"></a>Funções de previsão gerais (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Você pode usar a instrução **Select** em DMX (extensões de mineração de dados) para criar diferentes tipos de consultas. Uma consulta pode ser usada para retornar informações sobre o próprio modelo de mineração, fazer novas previsões ou alterar o modelo treinando-o com novos dados. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]fornece uma variedade de funções especializadas que controlam o tipo de informações retornadas em uma consulta. Adicionando essas funções a uma consulta DMX, você pode recuperar estatísticas ou colunas de dados adicionais. No entanto, cada tipo de consulta e cada tipo modelo suporta apenas algumas funções.  
  
## <a name="common-functions"></a>Funções comuns  
 Você pode usar funções para ampliar os resultados retornados por um modelo de mineração. Você pode usar as seguintes funções para qualquer instrução **Select** que retorne uma expressão de tabela:  

:::row:::
    :::column:::
        [&#41;&#40;DMX BottomCount](../dmx/bottomcount-dmx.md)  
        [&#41;&#40;DMX BottomPercent](../dmx/bottompercent-dmx.md)  
        [Prever &#40;DMX&#41;](../dmx/predict-dmx.md)  
        [&#41;&#40;DMX RangeMax](../dmx/rangemax-dmx.md)  
        [&#41;&#40;DMX RangeMid](../dmx/rangemid-dmx.md)  
    :::column-end:::
    :::column:::
        [&#41;&#40;DMX RangeMin](../dmx/rangemin-dmx.md)  
        [&#41;&#40;DMX TopCount](../dmx/topcount-dmx.md)  
        [&#41;&#40;DMX TopPercent](../dmx/toppercent-dmx.md)  
        [TopSum &#40;&#41;DMX](../dmx/topsum-dmx.md)  
    :::column-end:::
:::row-end:::

 Além disso, as funções a seguir são suportadas em quase todos os tipos de modelo:  
  
-   [Existe &#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [&#41;&#40;DMX IsTestCase](../dmx/istestcase-dmx.md)  
  
-   [&#41;&#40;DMX IsTrainingCase](../dmx/istrainingcase-dmx.md)  
  
-   [Prever &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [&#41;&#40;DMX RangeMax](../dmx/rangemax-dmx.md)  
  
-   [&#41;&#40;DMX RangeMid](../dmx/rangemid-dmx.md)  
  
-   [&#41;&#40;DMX RangeMin](../dmx/rangemin-dmx.md)  
  
-   [&#41;&#40;DMX StructureColumn](../dmx/structurecolumn-dmx.md)  
  
 Os algoritmos individuais podem dar suporte a funções adicionais. Para obter uma lista das funções com suporte em cada tipo de modelo, consulte [consultas de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).  
  
## <a name="functions-specific-to-select-syntax"></a>Funções específicas da sintaxe SELECT  
 A tabela a seguir lista as funções que você pode usar para cada tipo de instrução **Select** .  
  
 Para obter informações gerais sobre as funções no DMX, consulte [Data Mining Extensions &#40;&#41; referência de função DMX](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo de consulta|Funções suportadas|Comentários|  
|----------------|-------------------------|-------------|  
|[SELECIONAR DISTINCT DE\<model>](../dmx/select-distinct-from-model-dmx.md)|[&#41;&#40;DMX RangeMin](../dmx/rangemin-dmx.md)<br /><br /> [&#41;&#40;DMX RangeMid](../dmx/rangemid-dmx.md)<br /><br /> [&#41;&#40;DMX RangeMax](../dmx/rangemax-dmx.md)|Essas funções podem ser usadas para fornecer valores máximos, valores mínimos e médias para qualquer coluna que contenha tipos de dados numéricos, independentemente de a coluna ser contínua ou ter sido diferenciada.|  
|[Selecione \<model> . DISPUTA](../dmx/select-from-model-content-dmx.md)<br /><br /> ou<br /><br /> [Selecione \<model> . DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Essa função recupera nós filho para o nó especificado no modelo e pode ser usada, por exemplo, para iterar através de nós no conteúdo do modelo de mineração. A organização dos nós no conteúdo do modelo de mineração depende do tipo de modelo. Para obter informações sobre a estrutura de cada tipo de modelo de mineração, consulte [conteúdo do modelo de mineração &#40;&#41;de mineração de dados Analysis Services ](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).<br /><br /> Se você salvou o conteúdo do modelo de mineração como uma dimensão, também poderá usar outras funções MDX (Multidimensional Expressions) que estão disponíveis para consultar uma hierarquia de atributo.|  
|[Selecione \<model> . BOLSAS](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [Classe ClientSettingsGeneralFlag](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [&#41;&#40;DMX IsTrainingCase](../dmx/istrainingcase-dmx.md)<br /><br /> [&#41;&#40;DMX IsTestCase](../dmx/istestcase-dmx.md)|A função Lag tem suporte apenas para modelos de série temporal.<br /><br /> A função IsTestCase tem suporte em modelos baseados em uma estrutura que foi criada usando a opção de controle para criar um conjunto de dados de teste. Se o modelo não for baseado em uma estrutura com um conjunto de teste de validação, todos os casos serão considerados como casos de treinamento.|  
|[Selecione \<model> . SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|Nesse contexto, a função IsInNode retorna um caso que pertence a um conjunto de casos de exemplo ideais.|  
|Selecione \<model> . PMML|Não aplicável. Em vez disso, use funções de consulta XML.|As representações PMML são suportadas apenas pelos tipos de modelo a seguir:<br /><br /> Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)]<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering|  
|[SELECIONAR da \<model> junção de previsão](../dmx/select-from-model-prediction-join-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista de funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
|[SELECIONAR DE\<model>](../dmx/select-from-model-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista de funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
