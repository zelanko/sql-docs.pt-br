---
title: (DMX) os sinalizadores de modelagem | Microsoft Docs
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
- REGRESSOR flag
- DMX [Analysis Services], modeling flags
- MODEL_EXISTENCE_ONLY flag
- modeling flags [DMX]
- Data Mining Extensions [Analysis Services], modeling flags
- flags [DMX]
- NOT NULL flag
ms.assetid: 498d25f7-9597-47ae-8717-61ddd1d2fd15
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d7d762425310722d53de8c8bd7e92f497a334c78
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="modeling-flags-dmx"></a>Sinalizadores de modelagem (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Use sinalizadores de modelagem no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para fornecer informações adicionais para um algoritmo de mineração de dados sobre os dados definidos em uma tabela de casos. O algoritmo pode usar essas informações para criar um modelo de mineração de dados mais preciso. É possível definir sinalizadores de modelagem em colunas de estrutura de mineração e em colunas de modelo de mineração.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte aos seguintes sinalizadores de modelagem:  
  
 **NOT NULL**  
 Os valores da coluna de atributo não devem jamais conter um valor nulo. Ocorrerá um erro se o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encontrar um valor nulo nessa coluna de atributo durante o processo de treinamento do modelo. Esse sinalizador é definido em uma coluna de estrutura de mineração.  
  
 **REGRESSOR**  
 Indica que o algoritmo pode usar a coluna especificada na fórmula de regressão de algoritmos de regressão. Esse sinalizador tem suporte nos algoritmos [!INCLUDE[msCoName](../includes/msconame-md.md)]Regressão linear[!INCLUDE[msCoName](../includes/msconame-md.md)] e Árvores de decisão, sendo definido em uma coluna de modelo de mineração.  
  
 **MODEL_EXISTENCE_ONLY**  
 Os valores da coluna de atributo são menos importantes que a presença do atributo. Esse sinalizador é definido em uma coluna de modelo de mineração.  
  
 Os algoritmos de terceiros podem oferecer suporte a sinalizadores de modelagem adicionais. Para determinar os sinalizadores de modelagem um algoritmo oferece suporte, use o **SUPPORTED_MODELING_FLAGS** de linhas de esquema. Também é possível consultar os serviços de mineração no servidor para determinar quais sinalizadores de modelagem têm suporte para um determinado algoritmo. Por exemplo, a consulta a seguir retorna os sinalizadores de modelagem com suporte do algoritmo Regressão Linear da Microsoft no servidor atual:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Resultados esperados:  
  
 NOT NULL, REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Especificando sinalizadores de modelagem em um modelo de mineração  
 Para obter exemplos da sintaxe que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte para especificar um sinalizador em uma coluna de estrutura de mineração, consulte [criar estrutura de MINERAÇÃO &#40; DMX &#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para obter um exemplo da sintaxe para especificar um sinalizador de modelagem em uma coluna de modelo de mineração, consulte [ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md).  
  
 Para obter mais informações sobre como trabalhar com colunas do modelo de mineração, consulte [colunas do modelo de mineração](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40; Analysis Services – mineração de dados &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
