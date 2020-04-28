---
title: Referência do operador DMX (extensões de Data Mining) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e0dfafb74e6e86185872ea8e736b95dce7d4058
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68070907"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>Referência de operador de DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  A linguagem DMX (Data Mining Extensions) no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dá suporte a operadores aritméticos, de atribuição, de comparação, lógicos e unários. A tabela a seguir lista os operadores que a DMX suporta.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[+ &#40;adicionar&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Um operador aritmético que soma dois números.|  
|[-&#40;subtrair&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Operador aritmético que subtrai um número de outro.|  
|[&#42; &#40;multiplicar&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Operador aritmético que multiplica um número por outro.|  
|[&#40;dividir&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Operador aritmético que divide um número por outro.|  
|[&#60; &#40;menos de&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for menor que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62; &#40;maior que&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for maior que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[= &#40;igual a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;&#62; &#40;não é igual a&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for diferente do valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;= &#40;menor ou igual a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for menor ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62;= &#40;maior ou igual a&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for maior ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[E &#40;DMX&#41;](../dmx/and-dmx.md)|Operador lógico que executa uma conjunção ou duas expressões numéricas.|  
|[NÃO &#40;&#41;DMX](../dmx/not-dmx.md)|Operador lógico que executa uma negação em uma expressão numérica.|  
|[OU &#40;&#41;DMX](../dmx/or-dmx.md)|Operador lógico que executa uma disjunção em duas expressões numéricas.|  
|[+ &#40;positivo&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|Operador unário que retorna um valor positivo de expressão numérica.|  
|[-&#40;&#41; &#40;DMX negativo&#41;](../dmx/negative-dmx.md)|Operador unário que retorna um valor negativo de expressão numérica.|  
|[&#40;comentário de barra dupla&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. É possível aninhar comentários dentro de uma instrução DMX, incluí-los ao final de uma linha de código ou inseri-los em uma linha separada.|  
|[--Comentário de &#40;&#41; &#40;Resumo de&#41; do DMX](../dmx/comment-dmx-summary.md)|Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. É possível aninhar comentários dentro de uma instrução DMX, incluí-los ao final de uma linha de código ou inseri-los em uma linha separada.|  
|[Barra em estrela &#40;comentário&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. É possível aninhar comentários dentro de uma instrução DMX, incluí-los ao final de uma linha de código ou inseri-los em uma linha separada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)  
  
  
