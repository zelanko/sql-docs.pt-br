---
title: "Referência de operador MDX (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1cdb8c31-a5f6-4430-b509-f81344f4622a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a7178882592492f2447b802ff88bdf5c8b902be5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-operator-reference-mdx"></a>Referência de operador de MDX (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A linguagem MDX oferece suporte para aritmética, lógica, comparações, conjuntos, cadeias de caracteres e operadores unários. A tabela a seguir lista os operadores com suporte e suas descrições.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[– &#40; Comentário &#41; &#40; MDX &#41;](../mdx/comment-mdx-operator-reference.md)|Indica o texto de comentário fornecido pelo usuário.|  
|[-&#40; Exceto &#41; &#40; MDX &#41;](../mdx/except-mdx-operator.md)|Executa uma operação definida que retorna a diferença entre dois conjuntos, removendo membros duplicados.|  
|[-&#40; Negativo &#41; &#40; MDX &#41;](../mdx/negative-mdx.md)|Executa uma operação unária que retorna o valor negativo de uma expressão numérica.|  
|[-&#40; Subtrair &#41; &#40; MDX &#41;](../mdx/subtract-mdx.md)|Realiza uma operação aritmética que subtrai um número do outro.|  
|[&#42; &#40; Crossjoin &#41; &#40; MDX &#41;](../mdx/crossjoin-mdx-operator-reference.md)|Executa uma operação definida que retorna o produto cruzado de dois conjuntos.|  
|[&#42; &#40; Multiplique &#41; &#40; MDX &#41;](../mdx/multiply-mdx.md)|Realiza uma operação aritmética que multiplica dois números.|  
|[&#40; divisão &#41; &#40; MDX &#41;](../mdx/divide-mdx-operator-reference.md)|Realiza uma operação aritmética que divide um número por outro.|  
|[^ &#40; Energia &#41; &#40; MDX &#41;](../mdx/power-mdx.md)|Executa uma operação aritmética que eleva um número por outro.|  
|[Comentário &#40; MDX &#41;](../mdx/comment-mdx.md)|Indica o texto de comentário fornecido pelo usuário.|  
|[&#40; Comentário &#41; &#40; MDX &#41;](../mdx/comment-mdx-double-slash.md)|Indica texto fornecido pelo usuário.|  
|[: &#40; Intervalo de &#41; &#40; MDX &#41;](../mdx/range-mdx.md)|Executa uma operação definida que retorna um conjunto ordenado naturalmente, com dois membros especificados como pontos de extremidade, e todos os membros entre os dois membros especificados incluídos como membros do conjunto.|  
|[+ &#40; Adicionar &#41; &#40; MDX &#41;](../mdx/add-mdx.md)|Realiza uma operação aritmética que adiciona dois números.|  
|[+ &#40; Positivo &#41; &#40; MDX &#41;](../mdx/positive-mdx.md)|Executa uma operação unária que retorna o valor positivo de uma expressão numérica.|  
|[+ &#40; Concatenação de cadeia de caracteres &#41; &#40; MDX &#41;](../mdx/string-concatenation-mdx.md)|Executa uma operação de cadeia de caracteres que concatena duas ou mais cadeias de caracteres, tuplas ou uma combinação de cadeias de caracteres e tuplas.|  
|[+ &#40; União &#41; &#40; MDX &#41;](../mdx/union-mdx-operator-reference.md)|Executa uma operação de definição que retorna uma união de dois conjuntos, removendo as duplicações.|  
|[&#60; &#40; Menor &#41; &#40; MDX &#41;](../mdx/less-than-mdx.md)|Realiza uma operação de comparação que determina se o valor de uma linguagem MDX é menor do que o valor de outra linguagem MDX.|  
|[&#60; = &#40; Menor ou igual a &#41; &#40; MDX &#41;](../mdx/less-than-or-equal-to-mdx.md)|Realiza uma operação de comparação que determina se o valor de uma linguagem MDX é menor ou igual ao valor de outra linguagem MDX.|  
|[&#60; &#62; &#40; Não igual a &#41; &#40; MDX &#41;](../mdx/not-equal-to-mdx.md)|Realiza uma operação de comparação que determina se o valor de uma linguagem MDX é diferente do valor de outra linguagem MDX.|  
|[= &#40; Igual a &#41; &#40; MDX &#41;](../mdx/equal-to-mdx.md)|Realiza uma operação de comparação que determina se o valor de uma linguagem MDX é igual ao valor de outra linguagem MDX.|  
|[&#62; &#40; Maior &#41; &#40; MDX &#41;](../mdx/greater-than-mdx.md)|Realiza uma operação de comparação que determina se o valor de uma linguagem MDX é maior do que o valor de outra linguagem MDX.|  
|[&#62; = &#40; Maior que ou igual a &#41; &#40; MDX &#41;](../mdx/greater-than-or-equal-to-mdx.md)|Realiza uma operação de comparação que determina se o valor de uma linguagem MDX é maior ou igual ao valor de outra linguagem MDX.|  
|[E &#40; MDX &#41;](../mdx/and-mdx.md)|Realiza uma conjunção lógica em duas expressões numéricas.|  
|[FOR &#40; MDX &#41;](../mdx/is-mdx.md)|Executa uma comparação lógica em duas expressões de objeto.|  
|[NÃO &#40; MDX &#41;](../mdx/not-mdx.md)|Realiza uma negação lógica em uma expressão numérica.|  
|[OU &#40; MDX &#41;](../mdx/or-mdx.md)|Realiza uma disjunção lógica em duas expressões numéricas.|  
|[XOR &#40; MDX &#41;](../mdx/xor-mdx.md)|Executa uma exclusão lógica em duas expressões numéricas.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de linguagem MDX &#40; MDX &#41;](../mdx/mdx-language-reference-mdx.md)  
  
  

