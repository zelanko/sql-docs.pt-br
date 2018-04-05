---
title: Funções de previsão gerais (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- mapping functions to query types [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- SELECT statement [DMX]
- Data Mining Extensions [Analysis Services], functions
- Data Mining Extensions [Analysis Services], prediction queries
ms.assetid: e128159a-0458-43c9-bfe9-129cb6cfbe1c
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5e767d0243a8600c0f20cffebebfa92baffc2fc4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="general-prediction-functions-dmx"></a>Funções de previsão gerais (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar o **selecione** instrução em extensões DMX (Data Mining) para criar tipos diferentes de consultas. Uma consulta pode ser usada para retornar informações sobre o próprio modelo de mineração, fazer novas previsões ou alterar o modelo treinando-o com novos dados. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]Fornece uma variedade de funções especializadas que controlam o tipo de informação que é retornado em uma consulta. Adicionando essas funções a uma consulta DMX, você pode recuperar estatísticas ou colunas de dados adicionais. No entanto, cada tipo de consulta e cada tipo modelo suporta apenas algumas funções.  
  
## <a name="common-functions"></a>Funções comuns  
 Você pode usar funções para ampliar os resultados retornados por um modelo de mineração. Você pode usar as funções a seguir para qualquer **selecione** instrução que retorna uma expressão de tabela:  
  
|||  
|-|-|  
|[BottomCount &#40; DMX &#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40; DMX &#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40; DMX &#41;](../dmx/topcount-dmx.md)|  
|[Prever &#40; DMX &#41;](../dmx/predict-dmx.md)|[TopPercent &#40; DMX &#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)|[TopSum &#40; DMX &#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)||  
  
 Além disso, as funções a seguir são suportadas em quase todos os tipos de modelo:  
  
-   [Existe &#40; DMX &#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40; DMX &#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40; DMX &#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40; DMX &#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Prever &#40; DMX &#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40; DMX &#41;](../dmx/structurecolumn-dmx.md)  
  
 Os algoritmos individuais podem dar suporte a funções adicionais. Para obter uma lista das funções que são suportados por cada tipo de modelo, consulte [consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="functions-specific-to-select-syntax"></a>Funções específicas da sintaxe SELECT  
 A tabela a seguir lista as funções que você pode usar para cada tipo de **selecione** instrução.  
  
 Para obter informações gerais sobre funções em DMX, consulte [extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo de consulta|Funções suportadas|Remarks|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM \<modelo >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)|Essas funções podem ser usadas para fornecer valores máximos, valores mínimos e médias para qualquer coluna que contenha tipos de dados numéricos, independentemente de a coluna ser contínua ou ter sido diferenciada.|  
|[SELECT FROM \<modelo >. CONTEÚDO](../dmx/select-from-model-content-dmx.md)<br /><br /> ou em<br /><br /> [SELECT FROM \<modelo >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40; DMX &#41;](../dmx/isdescendant-dmx.md)|Essa função recupera nós filho para o nó especificado no modelo e pode ser usada, por exemplo, para iterar através de nós no conteúdo do modelo de mineração. A organização dos nós no conteúdo do modelo de mineração depende do tipo de modelo. Para obter informações sobre a estrutura de cada tipo de modelo de mineração, consulte [conteúdo do modelo de mineração &#40; Analysis Services – mineração de dados &#41; ](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).<br /><br /> Se você tiver salvo o conteúdo do modelo de mineração como uma dimensão, também poderá usar outras funções MDX que estão disponíveis para consultar uma hierarquia de atributo.|  
|[SELECT FROM \<modelo >. CASOS](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag Class](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40; DMX &#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40; DMX &#41;](../dmx/istestcase-dmx.md)|A função Lag é suportada somente para modelos de série temporal.<br /><br /> Há suporte para a função IsTestCase modelos com base em uma estrutura que foi criada usando a opção de validação para criar um conjunto de dados de teste. Se o modelo não for baseado em uma estrutura com um conjunto de teste de validação, todos os casos serão considerados como casos de treinamento.|  
|[SELECT FROM \<modelo >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)|Nesse contexto, a função IsInNode retornará um caso que pertence a um conjunto de casos de amostra idealizados.|  
|SELECT FROM \<modelo >. PMML|Não aplicável. Em vez disso, use funções de consulta XML.|As representações PMML são suportadas apenas pelos tipos de modelo a seguir:<br /><br /> Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)]<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering|  
|[SELECT FROM \<modelo > PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista de funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md).|  
|[SELECT FROM \<modelo >](../dmx/select-from-model-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista de funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
