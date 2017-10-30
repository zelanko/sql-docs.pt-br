---
title: Operadores de conjunto | Microsoft Docs
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
- set operators [MDX]
ms.assetid: 83500d2e-44b3-49eb-a221-3ce5a58277a5
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ed67b969d53eeb65009926cade623d2b87b9e175
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="set-operators"></a>Operadores de conjunto
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Na linguagem MDX, os operadores de conjunto executam operações em membros ou conjuntos e retornam um conjunto. Frequentemente você usa os operadores de conjunto como uma alternativa para várias funções de conjunto na linguagem MDX.  
  
 O MDX oferece suporte a operadores de conjunto listados na tabela a seguir.  
  
|Operador|Description|  
|--------------|-----------------|  
|[-(Exceto)](../mdx/except-mdx-operator.md)|Retorna a diferença entre dois conjuntos, removendo membros duplicados.<br /><br /> Esse operador é funcionalmente equivalente ao [exceto](../mdx/except-mdx-function.md) função.|  
|[* (Produto cruzado)](../mdx/crossjoin-mdx-operator-reference.md)|Retorna o produto cruzado de dois conjuntos.<br /><br /> Esse operador é funcionalmente equivalente ao [Crossjoin](../mdx/crossjoin-mdx.md) função.|  
|[: (Intervalo)](../mdx/range-mdx.md)|Retorna um conjunto ordenado naturalmente, com dois membros especificados como pontos de extremidade, e todos os membros entre os dois membros especificados incluídos como membros do conjunto.|  
|[+ (União)](../mdx/union-mdx-operator-reference.md)|Retorna uma união de dois conjuntos, exceto membros duplicados.<br /><br /> Esse operador é funcionalmente equivalente ao [união &#40; MDX &#41; ](../mdx/union-mdx.md) função.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40; Sintaxe MDX &#41;](../mdx/operators-mdx-syntax.md)  
  
  

