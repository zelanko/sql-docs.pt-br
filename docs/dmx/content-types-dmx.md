---
title: "Tipos (DMX) de conteúdo | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], content types
- content types [DMX]
- DMX [Analysis Services], content types
ms.assetid: ab9dd887-df8d-4878-96b0-635881892573
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 33af21a44066e96223bbfc07e39f4718edf87fc2
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="content-types-dmx"></a>Tipos de conteúdo (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Os algoritmos de mineração de dados requerem informações que vão além do tipo de dados para funcional corretamente, como tipo de conteúdo. O tipo de conteúdo ajuda o algoritmo a determinar como trabalhar com os dados na coluna.  
  
 Cada algoritmo oferece suporte a tipos de conteúdo específicos. Por exemplo, o algoritmo Naive Bayes do [!INCLUDE[msCoName](../includes/msconame-md.md)] não pode usar colunas contínuas. Para usar uma coluna contínua em um modelo [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, é preciso diferenciar os dados na coluna. Alguns algoritmos requerem determinados tipos de conteúdo para funcionar corretamente. Por exemplo, o algoritmo Times Series do [!INCLUDE[msCoName](../includes/msconame-md.md)] exige uma coluna de chave de tempo para identificação do período em que os dados foram coletados.  
  
 Para tipos de uma descrição completa do conteúdo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte, consulte [tipos de conteúdo &#40; mineração de dados &#41;](../analysis-services/data-mining/content-types-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Noções básicas sobre a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

