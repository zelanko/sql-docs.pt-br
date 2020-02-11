---
title: WTD (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eee40829c72394bf95a1bc06540a434a1c74e166
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125807"
---
# <a name="wtd-mdx"></a>Wtd (MDX)


  Retorna um conjunto de membros irmãos do mesmo nível como um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo nível Semana na dimensão Tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão de membro não for especificada, o padrão será o membro atual da primeira hierarquia com um nível do tipo Weeks na primeira dimensão do tipo time (**time. CurrentMember**) no grupo de medidas.  
  
 A função **WTD** é uma função de atalho para a função [PeriodsToDate](../mdx/periodstodate-mdx.md) em que o nível é definido como *semanas*. Ou seja, `Wtd(Member_Expression)` é equivalente a `PeriodsToDate(Week_Level_Expression,Member_Expression)`.  
  
## <a name="see-also"></a>Consulte Também  
 [Qtd &#40;&#41;MDX](../mdx/qtd-mdx.md)   
 [MTD&#41;MDX &#40;](../mdx/mtd-mdx.md)   
 [&#40;do MDX&#41;no ano](../mdx/ytd-mdx.md)   
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
