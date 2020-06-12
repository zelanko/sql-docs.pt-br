---
title: Operadores de comparação (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05bb9bc1ad4dfeed1cf2747a8d5bb854fec8d9af
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669705"
---
# <a name="operators---comparison"></a>Operadores – comparação
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar operadores de comparação com dados escalares em qualquer expressão DMX (Data Mining Extensions) no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Os operadores de comparação são avaliados como um tipo de dados booliano; elas retornam TRUE ou FALSE com base no resultado da condição testada.  
  
 A tabela a seguir identifica os operadores de comparação aos quais a DMX oferece suporte.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[&#60; &#40;menos de&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for menor que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62; &#40;maior que&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for maior que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[= &#40;igual a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;&#62; &#40;não é igual a&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for diferente do valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;= &#40;menor ou igual a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for menor ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62;= &#40;maior ou igual a&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for maior ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
  
 É igualmente possível usar operadores de comparação em instruções e funções DMX para procurar uma condição.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expressões &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
