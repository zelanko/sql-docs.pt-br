---
title: Operadores (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 072d0a36a4803f4de1d50ba066e4e86e5d171c5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502047"
---
# <a name="operators-dmx"></a>Operadores (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar operadores de extensões DMX (Data Mining) para realizar a aritmética, comparação, concatenação e operações lógicas em uma consulta no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa os operadores para executar as seguintes ações:  
  
-   Pesquisar valores ou objetos que atendem a uma condição específica.  
  
-   Implementar uma decisão entre valores ou expressões.  
  
 O DMX usa várias categorias de operadores, descritas nas seções a seguir. Para obter informações adicionais sobre operadores individuais, consulte [extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
|Categoria de operador|Tipo de operação|  
|-----------------------|-----------------------|  
|[Operadores aritméticos &#40;DMX&#41;](../dmx/operators-arithmetic.md)|Realiza adição, subtração, multiplicação ou divisão.|  
|[Operadores de comparação &#40;DMX&#41;](../dmx/operators-comparison.md)|Comparam um valor contra outro valor ou contra uma expressão.|  
|[Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)|Testam a legitimidade de uma condição, como AND, OR ou NOT.|  
|[Operadores unários &#40;DMX&#41;](../dmx/operators-unary.md)|Executam uma operação em um operando único.|  
  
 Use os operadores para combinar expressões menores em DMX em expressões mais complexas. Em expressões complexas, os operadores são avaliados em ordem, com base na definição [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de prioridade do operador. Os operadores com alta prioridade são executados antes dos operadores com prioridade baixa. Para obter mais informações sobre expressões, consulte [expressões &#40;DMX&#41;](../dmx/expressions-dmx.md).  
  
 Quando expressões simples são combinadas para formar uma expressão complexa, o tipo de dados da expressão resultante é determinado pela combinação das regras para operadores com as regras de prioridade para o tipo de dados. Se o resultado for um caractere ou um valor Unicode, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] determinará a ordenação do resultado pela combinação das regras para os operadores com as regras para prioridade de ordenação. Há também regras que determinam a precisão, a escala e a extensão do resultado, com base na precisão, na escala e na extensão das expressões simples.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
