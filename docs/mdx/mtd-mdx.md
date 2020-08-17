---
description: Mtd (MDX)
title: MTD (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 398503bc60be44a0a5fcbcc329f3c455df967d7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341373"
---
# <a name="mtd-mdx"></a>Mtd (MDX)


  Retorna um conjunto de membros irmão do mesmo nível como um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo nível Ano na dimensão Tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão de membro não for especificada, o padrão será o membro atual da primeira hierarquia com um nível do tipo *months* na primeira dimensão do tipo *time* no grupo de medidas.  
  
 A função **MTD** é uma função de atalho para a função [PeriodsToDate](../mdx/periodstodate-mdx.md) quando a propriedade Type da hierarquia de atributo na qual um nível é baseado é definida como *meses*. Ou seja, `Mtd(Member_Expression)` é equivalente a `PeriodsToDate(Month_Level_Expression,Member_Expression)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a soma dos custos de frete do mês até a data para vendas pela Internet para o mês de julho de 2002 até o dia 20 de julho.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sum &#40;&#41;MDX ](../mdx/sum-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
