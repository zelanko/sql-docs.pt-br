---
description: Função Current (MDX)
title: Atual (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 105bb306cb84f151024a288f5aa15eb09ddbf5c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387542"
---
# <a name="current-mdx"></a>Função Current (MDX)


  Retorna a tupla atual de um conjunto durante a iteração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 Em cada etapa durante uma iteração, a tupla que está sendo operada em é a tupla atual. A função **atual** retorna essa tupla. Essa função só é válida durante uma iteração em um conjunto.  
  
 As funções MDX que iteram por meio de um conjunto incluem a função [Generate](../mdx/generate-mdx.md) .  
  
> [!NOTE]  
>  Essa função funciona somente com conjuntos que são nomeados, seja usando um alias de conjunto ou definindo um conjunto nomeado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como usar a função **atual** dentro da **geração**:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
