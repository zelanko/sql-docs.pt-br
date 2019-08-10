---
title: Valor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f373f626d778c4d77ec5843dca5bb11da728451d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887444"
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
 A função **Value** retorna o valor do membro especificado como uma cadeia de caracteres. O argumento de **valor** é opcional porque o valor de um membro é a propriedade padrão de um membro e é o valor retornado para um membro se nenhum outro valor for especificado. Para obter mais informações sobre as propriedades de membros, consulte [Propriedades &#40;intrínsecas do membro MDX&#41; ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) e propriedades [ &#40;do&#41;membro definidas pelo usuário MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [&#40;MDX MemberValue&#41;](../mdx/membervalue-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [Nome &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
