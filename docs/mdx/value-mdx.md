---
description: Value (MDX)
title: Valor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 52224625f5e2e6fc70ca9a76f750ed374108c52c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196724"
---
# <a name="value-mdx"></a>Value (MDX)


  Retorna o valor do membro atual da dimensão Medidas que faz interseções com o membro atual das hierarquias do atributo no contexto da consulta.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 A função **Value** retorna o valor do membro especificado como uma cadeia de caracteres. O argumento de **valor** é opcional porque o valor de um membro é a propriedade padrão de um membro e é o valor retornado para um membro se nenhum outro valor for especificado. Para obter mais informações sobre as propriedades de membros, consulte [propriedades intrínsecas do membro &#40;mdx&#41;](/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) e [Propriedades do membro definidas pelo usuário &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o valor de um membro e também retorna explicitamente o nome dele.  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 O exemplo a seguir retorna o valor de um membro como o valor padrão que é retornado para um membro em um eixo.  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [Propriedades &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [Nome &#40;&#41;MDX ](../mdx/name-mdx.md)   
 [UniqueName&#41;MDX &#40;](../mdx/uniquename-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
