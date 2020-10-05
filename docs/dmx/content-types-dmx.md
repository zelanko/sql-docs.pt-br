---
description: Tipos de conteúdo (DMX)
title: Tipos de conteúdo (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b1a400e5247cc812cb72ba3422cb361888342155
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726294"
---
# <a name="content-types-dmx"></a>Tipos de conteúdo (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Os algoritmos de mineração de dados requerem informações que vão além do tipo de dados para funcional corretamente, como tipo de conteúdo. O tipo de conteúdo ajuda o algoritmo a determinar como trabalhar com os dados na coluna.  
  
 Cada algoritmo oferece suporte a tipos de conteúdo específicos. Por exemplo, o algoritmo Naive Bayes do [!INCLUDE[msCoName](../includes/msconame-md.md)] não pode usar colunas contínuas. Para usar uma coluna contínua em um modelo [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, é preciso diferenciar os dados na coluna. Alguns algoritmos requerem determinados tipos de conteúdo para funcionar corretamente. Por exemplo, o algoritmo Times Series do [!INCLUDE[msCoName](../includes/msconame-md.md)] exige uma coluna de chave de tempo para identificação do período em que os dados foram coletados.  
  
 Para obter uma descrição completa dos tipos de conteúdo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] aos quais o oferece suporte, consulte [tipos de conteúdo &#40;mineração de dados&#41;](/analysis-services/data-mining/content-types-data-mining).  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
