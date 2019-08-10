---
title: Uso (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b961282ba6bc25caa260a3e156f843a413a5ef1a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893108"
---
# <a name="usage-dmx"></a>Uso (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ao usar o DMX (extensões de mineração de dados) para definir um novo modelo [!INCLUDE[msCoName](../includes/msconame-md.md)] de Data Mining no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você deve especificar como o algoritmo de Data Mining que cria o modelo usará cada coluna. Especifique as colunas como um dos tipos seguintes:  
  
-   **Chave**  
  
-   **Sequência de chaves**  
  
-   **Key Time**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 As colunas deixadas sem-especificação em DMX são tratadas como colunas de entrada.  
  
 Para processar corretamente um modelo, o algoritmo precisará saber quais colunas são a coluna de chave que identifica exclusivamente cada uma das linhas; qual coluna é a coluna de destino para a criação de previsões, caso se esteja criando um modelo previsível, e quais colunas usar como colunas de entrada para criar relações que preveem a coluna de destino.  
  
 As colunas especificadas como o tipo de **previsão** são usadas como colunas de entrada e de saída. As colunas especificadas como **PredictOnly** são usadas apenas como colunas de saída. Os algoritmos específicos podem tratar as colunas Predict de forma diferente.  
  
 Para obter mais informações sobre os tipos de uso [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de coluna que o suporta, consulte [colunas do modelo de mineração](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Elementos de sintaxe &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referência da função &#40;DMX&#41; das extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenções de sintaxe &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções &#40;de previsão gerais DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
