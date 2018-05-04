---
title: Referência Data Mining Extensions (DMX) operador | Microsoft Docs
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
- operators [DMX]
- DMX [Analysis Services], operators
- Data Mining Extensions [Analysis Services], operators
ms.assetid: a6d747c0-9ff0-475f-86cd-34bebd79c21a
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5b833a7a5f6b6d1329a1dc7a738a163efde2c0ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>Referência de operador de DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  A linguagem de extensões DMX (Data Mining) [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte aos operadores de aritmética, atribuição, comparação, lógicos e unário. A tabela a seguir lista os operadores que a DMX suporta.  
  
|Operador|Description|  
|--------------|-----------------|  
|[+ &#40;Adicionar&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Um operador aritmético que soma dois números.|  
|[- &#40;Subtrair&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Operador aritmético que subtrai um número de outro.|  
|[&#42;&#40;Multiplicar&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Operador aritmético que multiplica um número por outro.|  
|[&#40;Dividir&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Operador aritmético que divide um número por outro.|  
|[&#60;&#40;Menor&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for menor que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62;&#40;Maior&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for maior que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[= &#40;Igual a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;&#62;&#40;Não é igual a&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for diferente do valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60;= &#40;Menor ou igual a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for menor ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62;= &#40;Maior que ou igual a&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Operador de comparação. Para argumentos que avaliam valores não nulos; que retornam TRUE se o valor do argumento da esquerda for maior ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[E &AMP;#40;DMX&AMP;#41;](../dmx/and-dmx.md)|Operador lógico que executa uma conjunção ou duas expressões numéricas.|  
|[NÃO &AMP;#40;DMX&AMP;#41;](../dmx/not-dmx.md)|Operador lógico que executa uma negação em uma expressão numérica.|  
|[OU &AMP;#40;DMX&AMP;#41;](../dmx/or-dmx.md)|Operador lógico que executa uma disjunção em duas expressões numéricas.|  
|[+ &#40;Positivo&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|Operador unário que retorna um valor positivo de expressão numérica.|  
|[- &#40;Negativo&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|Operador unário que retorna um valor negativo de expressão numérica.|  
|[Barras duplas &#40;comentário&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. É possível aninhar comentários dentro de uma instrução DMX, incluí-los ao final de uma linha de código ou inseri-los em uma linha separada.|  
|[– &#40;Comentário&#41; &#40;DMX&#41; resumo](../dmx/comment-dmx-summary.md)|Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. É possível aninhar comentários dentro de uma instrução DMX, incluí-los ao final de uma linha de código ou inseri-los em uma linha separada.|  
|[Estrela de barra &#40;comentário&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|Indica uma cadeia de caracteres de texto que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não deve executar. É possível aninhar comentários dentro de uma instrução DMX, incluí-los ao final de uma linha de código ou inseri-los em uma linha separada.|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
