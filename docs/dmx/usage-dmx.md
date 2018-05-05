---
title: Uso (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- column usage [DMX]
- Data Mining Extensions [Analysis Services], column usage types
- DMX [Analysis Services], column usage types
ms.assetid: 6d7ae72a-f5b5-4744-a3a2-46ccd6432c1a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c4235e6b839ecd8762e935151e7b86f278f97912
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
