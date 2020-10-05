---
description: Sinalizadores de modelagem (DMX)
title: Sinalizadores de modelagem (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 968b1c10f8eb054f6527253bd358e97eaa396637
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727717"
---
# <a name="modeling-flags-dmx"></a>Sinalizadores de modelagem (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Use sinalizadores de modelagem no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para fornecer informações adicionais para um algoritmo de mineração de dados sobre os dados definidos em uma tabela de casos. O algoritmo pode usar essas informações para criar um modelo de mineração de dados mais preciso. É possível definir sinalizadores de modelagem em colunas de estrutura de mineração e em colunas de modelo de mineração.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte aos seguintes sinalizadores de modelagem:  
  
 **NOT NULL**  
 Os valores da coluna de atributo não devem jamais conter um valor nulo. Ocorrerá um erro se o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encontrar um valor nulo nessa coluna de atributo durante o processo de treinamento do modelo. Esse sinalizador é definido em uma coluna de estrutura de mineração.  
  
 **REGRESSOR**  
 Indica que o algoritmo pode usar a coluna especificada na fórmula de regressão de algoritmos de regressão. Esse sinalizador tem suporte nos algoritmos [!INCLUDE[msCoName](../includes/msconame-md.md)]Regressão linear[!INCLUDE[msCoName](../includes/msconame-md.md)] e Árvores de decisão, sendo definido em uma coluna de modelo de mineração.  
  
 **MODEL_EXISTENCE_ONLY**  
 Os valores da coluna de atributo são menos importantes que a presença do atributo. Esse sinalizador é definido em uma coluna de modelo de mineração.  
  
 Os algoritmos de terceiros podem oferecer suporte a sinalizadores de modelagem adicionais. Para determinar quais sinalizadores de modelagem são compatíveis com um algoritmo, use o conjunto de linhas de esquema **SUPPORTED_MODELING_FLAGS** . Também é possível consultar os serviços de mineração no servidor para determinar quais sinalizadores de modelagem têm suporte para um determinado algoritmo. Por exemplo, a consulta a seguir retorna os sinalizadores de modelagem com suporte do algoritmo Regressão Linear da Microsoft no servidor atual:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Resultados esperados:  
  
 NOT NULL, REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Especificando sinalizadores de modelagem em um modelo de mineração  
 Para obter exemplos da sintaxe que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dá suporte para especificar um sinalizador em uma coluna de estrutura de mineração, consulte [criar estrutura de mineração &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para obter um exemplo da sintaxe para especificar um flga de modelagem em uma coluna de modelo de mineração, consulte [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
 Para obter mais informações sobre como trabalhar com colunas do modelo de mineração, consulte [colunas do modelo de mineração](/analysis-services/data-mining/mining-model-columns).  
  
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
  
