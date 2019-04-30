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
manager: kfile
ms.openlocfilehash: 6eb91bb43407311a58e495b5f9391186821d3a67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251421"
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
 O **valor** função retorna o valor do membro especificado como uma cadeia de caracteres. O **valor** argumento é opcional porque o valor de um membro é a propriedade padrão de um membro e é o valor retornado para um membro se nenhum outro valor for especificado. Para obter mais informações sobre as propriedades de membros, consulte [propriedades intrínsecas do membro &#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) e [propriedades do membro definidas pelo usuário &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
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
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [Name &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
