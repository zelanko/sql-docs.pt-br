---
title: "Operadores de comparação (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- comparison operators [DMX]
ms.assetid: eea3cf90-9683-4453-b1f3-da740f3a4885
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92362f5158b23b0425030092fe7b9372a08b13ca
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="operators---comparison"></a>Operadores - comparação
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Você pode usar operadores de comparação com dados escalares em qualquer expressão extensões DMX (Data Mining) em [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Operadores de comparação avaliam um tipo de dados booleano; elas retornam TRUE ou FALSE com base no resultado da condição testada.  
  
 A tabela a seguir identifica os operadores de comparação aos quais a DMX oferece suporte.  
  
|Operador|Description|  
|--------------|-----------------|  
|[&#60; &#40; Menor &#41; &#40; DMX &#41;](../dmx/less-than-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for menor que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62; &#40; Maior &#41; &#40; DMX &#41;](../dmx/greater-than-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for maior que o valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[= &#40; Igual a &#41; &#40; DMX &#41;](../dmx/equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60; &#62; &#40; Não igual a &#41; &#40; DMX &#41;](../dmx/not-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for diferente do valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#60; = &#40; Menor ou igual a &#41; &#40; DMX &#41;](../dmx/less-than-or-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for menor ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[&#62; = &#40; Maior que ou igual a &#41; &#40; DMX &#41;](../dmx/greater-than-or-equal-to-dmx.md)|Para argumentos que avaliam um valor não nulo; que retornam TRUE se o valor do argumento da esquerda for maior ou igual ao valor do argumento da direita; que retornam FALSE se for o contrário. Se um ou ambos os argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
  
 É igualmente possível usar operadores de comparação em instruções e funções DMX para procurar uma condição.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expressões &#40; DMX &#41;](../dmx/expressions-dmx.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Noções básicas sobre a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  

