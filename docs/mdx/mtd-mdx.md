---
title: MTD (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e38d8d3485e50054ee4d1106b1ef7bdfc8ce96ea
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580758"
---
# <a name="mtd-mdx"></a>Mtd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto de membros irmão do mesmo nível como um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo nível Ano na dimensão Tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 Se uma expressão de membro não for especificada, o padrão será o membro atual da primeira hierarquia com um nível de tipo *meses* na primeira dimensão do tipo *tempo* no grupo de medidas.  
  
 O **Mtd** é uma função de atalho para o [PeriodsToDate](../mdx/periodstodate-mdx.md) funciona quando a propriedade de tipo da hierarquia de atributo no qual um nível é baseado é definida como *meses*. Ou seja, `Mtd(Member_Expression)` é equivalente a `PeriodsToDate(Month_Level_Expression,Member_Expression)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a soma do mês custos de frete de data de vendas pela Internet para o mês de julho de 2002 até o dia 20 de julho.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Soma &#40;MDX&#41;](../mdx/sum-mdx.md)   
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
