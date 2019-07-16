---
title: Operadores de comparação (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fcbfb95070783db002d34870e5508df5322210d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008203"
---
# <a name="operators---comparison"></a>Operadores – comparação
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar operadores de comparação com dados escalares em qualquer expressão de extensões DMX (Data Mining) em [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Operadores de comparação avaliam um tipo de dados Boolean; elas retornam TRUE ou FALSE com base no resultado da condição testada.  
  
 A tabela a seguir identifica os operadores de comparação aos quais a DMX oferece suporte.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[&#60;&#40;Menor que&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for menor que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62;&#40;Maior que&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for maior que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[= &#40;Igual a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;&#62;&#40;Não é igual a&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for diferente do valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;= &#40;Menor que ou igual a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for menor ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62;= &#40;Maior que ou igual a&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for maior ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
  
 É igualmente possível usar operadores de comparação em instruções e funções DMX para procurar uma condição.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expressions &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
