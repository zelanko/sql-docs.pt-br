---
description: Operadores (DMX)
title: Operadores (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c523ea9150f7d3361f93582e01b703be35d2366
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395732"
---
# <a name="operators-dmx"></a>Operadores (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Você pode usar os operadores DMX (Data Mining Extensions) para executar operações aritméticas, de comparação, de concatenação e lógicas em uma consulta no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa os operadores para executar as seguintes ações:  
  
-   Pesquise por valores ou objetos que atendam a uma condição específica.  
  
-   Implementar uma decisão entre valores ou expressões.  
  
 O DMX usa várias categorias de operadores, descritas nas seções a seguir. Para obter informações adicionais sobre operadores individuais, consulte [Data Mining Extensions &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
|Categoria de operador|Tipo de operação|  
|-----------------------|-----------------------|  
|[Operadores aritméticos &#40;&#41;DMX ](../dmx/operators-arithmetic.md)|Realiza adição, subtração, multiplicação ou divisão.|  
|[Operadores de comparação &#40;&#41;DMX ](../dmx/operators-comparison.md)|Comparam um valor contra outro valor ou contra uma expressão.|  
|[Operadores lógicos &#40;&#41;DMX ](../dmx/operators-logical.md)|Testam a legitimidade de uma condição, como AND, OR ou NOT.|  
|[Operadores unários &#40;DMX&#41;](../dmx/operators-unary.md)|Executam uma operação em um operando único.|  
  
 Use os operadores para combinar expressões menores em DMX em expressões mais complexas. Em expressões complexas, os operadores são avaliados em ordem, com base na definição [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de prioridade do operador. Os operadores com alta prioridade são executados antes dos operadores com prioridade baixa. Para obter mais informações sobre expressões, consulte [expressions &#40;DMX&#41;](../dmx/expressions-dmx.md).  
  
 Quando expressões simples são combinadas para formar uma expressão complexa, o tipo de dados da expressão resultante é determinado pela combinação das regras para operadores com as regras de prioridade para o tipo de dados. Se o resultado for um caractere ou um valor Unicode, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] determinará a ordenação do resultado pela combinação das regras para os operadores com as regras para prioridade de ordenação. Há também regras que determinam a precisão, a escala e a extensão do resultado, com base na precisão, na escala e na extensão das expressões simples.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
