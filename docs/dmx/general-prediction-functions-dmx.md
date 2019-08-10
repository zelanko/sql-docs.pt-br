---
title: Funções de previsão gerais (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 57909c1bb4009ae85b7e1b38b8b3cf3fa0e70ea9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892769"
---
# <a name="general-prediction-functions-dmx"></a>Funções de previsão gerais (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar a instrução **Select** em DMX (extensões de mineração de dados) para criar diferentes tipos de consultas. Uma consulta pode ser usada para retornar informações sobre o próprio modelo de mineração, fazer novas previsões ou alterar o modelo treinando-o com novos dados. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]fornece uma variedade de funções especializadas que controlam o tipo de informações retornadas em uma consulta. Adicionando essas funções a uma consulta DMX, você pode recuperar estatísticas ou colunas de dados adicionais. No entanto, cada tipo de consulta e cada tipo modelo suporta apenas algumas funções.  
  
## <a name="common-functions"></a>Funções comuns  
 Você pode usar funções para ampliar os resultados retornados por um modelo de mineração. Você pode usar as seguintes funções para qualquer instrução **Select** que retorne uma expressão de tabela:  
  
|||  
|-|-|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Prever &#40;DMX&#41;](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[&#40;DMX de TopSum&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 Além disso, as funções a seguir são suportadas em quase todos os tipos de modelo:  
  
-   [Existe &#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Prever &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 Os algoritmos individuais podem dar suporte a funções adicionais. Para obter uma lista das funções com suporte em cada tipo de modelo, consulte [consultas de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).  
  
## <a name="functions-specific-to-select-syntax"></a>Funções específicas da sintaxe SELECT  
 A tabela a seguir lista as funções que você pode usar para cada tipo de instrução **Select** .  
  
 Para obter informações gerais sobre as funções no DMX, consulte [referência &#40;da&#41; função DMX das extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo de consulta|Funções suportadas|Comentários|  
|----------------|-------------------------|-------------|  
|[Selecione DISTINCT do \<modelo >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|Essas funções podem ser usadas para fornecer valores máximos, valores mínimos e médias para qualquer coluna que contenha tipos de dados numéricos, independentemente de a coluna ser contínua ou ter sido diferenciada.|  
|[Selecione do \<modelo >. DISPUTA](../dmx/select-from-model-content-dmx.md)<br /><br /> ou<br /><br /> [Selecione do \<modelo >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Essa função recupera nós filho para o nó especificado no modelo e pode ser usada, por exemplo, para iterar através de nós no conteúdo do modelo de mineração. A organização dos nós no conteúdo do modelo de mineração depende do tipo de modelo. Para obter informações sobre a estrutura de cada tipo de modelo de mineração, consulte [conteúdo &#40;do modelo de&#41;mineração Analysis Services-Mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).<br /><br /> Se você tiver salvo o conteúdo do modelo de mineração como uma dimensão, também poderá usar outras funções MDX que estão disponíveis para consultar uma hierarquia de atributo.|  
|[Selecione do \<modelo >. BOLSAS](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag Class](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|A função Lag tem suporte apenas para modelos de série temporal.<br /><br /> A função IsTestCase tem suporte em modelos baseados em uma estrutura que foi criada usando a opção de controle para criar um conjunto de dados de teste. Se o modelo não for baseado em uma estrutura com um conjunto de teste de validação, todos os casos serão considerados como casos de treinamento.|  
|[Selecione do \<modelo >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|Nesse contexto, a função IsInNode retorna um caso que pertence a um conjunto de casos de exemplo ideais.|  
|Selecione do \<modelo >. PMML|Não aplicável. Em vez disso, use funções de consulta XML.|As representações PMML são suportadas apenas pelos tipos de modelo a seguir:<br /><br /> Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)]<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering|  
|[Selecionar do \<modelo > junção de previsão](../dmx/select-from-model-prediction-join-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista de funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
|[Selecionar do \<modelo >](../dmx/select-from-model-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista de funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência da função &#40;DMX&#41; das extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenções de sintaxe &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Elementos de sintaxe &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
