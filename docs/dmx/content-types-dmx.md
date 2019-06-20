---
title: Tipos (DMX) de conteúdo | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 002dfef00f428f7fe87f3de06eb174e0566282c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62853490"
---
# <a name="content-types-dmx"></a>Tipos de conteúdo (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Os algoritmos de mineração de dados requerem informações que vão além do tipo de dados para funcional corretamente, como tipo de conteúdo. O tipo de conteúdo ajuda o algoritmo a determinar como trabalhar com os dados na coluna.  
  
 Cada algoritmo oferece suporte a tipos de conteúdo específicos. Por exemplo, o algoritmo Naive Bayes do [!INCLUDE[msCoName](../includes/msconame-md.md)] não pode usar colunas contínuas. Para usar uma coluna contínua em um modelo [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, é preciso diferenciar os dados na coluna. Alguns algoritmos requerem determinados tipos de conteúdo para funcionar corretamente. Por exemplo, o algoritmo Times Series do [!INCLUDE[msCoName](../includes/msconame-md.md)] exige uma coluna de chave de tempo para identificação do período em que os dados foram coletados.  
  
 Para tipos de que uma descrição completa do conteúdo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dá suporte, consulte [tipos de conteúdo &#40;mineração de dados&#41;](../analysis-services/data-mining/content-types-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
