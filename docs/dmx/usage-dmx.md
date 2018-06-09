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
manager: kfile
ms.openlocfilehash: 459d6a0240ac2588c0924eae7bdae348a71f5946
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841429"
---
# <a name="usage-dmx"></a>Uso (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quando você usa extensões DMX (Data Mining) para definir um novo modelo de mineração de dados no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você deve especificar como o algoritmo de mineração de dados que cria o modelo usará cada coluna. Especifique as colunas como um dos tipos seguintes:  
  
-   **Chave**  
  
-   **Sequência de teclas**  
  
-   **Chave de tempo**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 As colunas deixadas sem-especificação em DMX são tratadas como colunas de entrada.  
  
 Para processar corretamente um modelo, o algoritmo precisará saber quais colunas são a coluna de chave que identifica exclusivamente cada uma das linhas; qual coluna é a coluna de destino para a criação de previsões, caso se esteja criando um modelo previsível, e quais colunas usar como colunas de entrada para criar relações que preveem a coluna de destino.  
  
 Colunas que são especificadas como o **prever** tipo são usadas como colunas de entrada e saídas. Colunas que são especificadas como **PredictOnly** só são usadas como colunas de saída. Os algoritmos específicos podem tratar as colunas Predict de forma diferente.  
  
 Para obter mais informações sobre a coluna de uso de tipos que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte, consulte [colunas do modelo de mineração](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – mineração de dados&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
