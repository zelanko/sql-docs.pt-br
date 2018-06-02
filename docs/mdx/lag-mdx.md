---
title: Latência (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c5e019312eacc2cf3f842721054ad5e39ea75d4b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578858"
---
# <a name="lag-mdx"></a>Latência (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o membro que é um número especificado de posições antes de um membro especificado no nível do membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Index*  
 Uma expressão numérica válida que especifica o número de posições de membro a serem atrasadas.  
  
## <a name="remarks"></a>Remarks  
 As posições de membros em um nível são determinadas pela ordem natural da hierarquia de atributo. A numeração das posições se baseia em zero.  
  
 Se o retardo especificado for zero, o **latência** função retorna o próprio membro especificado.  
  
 Se o retardo especificado for negativo, o **latência** função retorna um membro subsequente.  
  
 `Lag(1)` é equivalente a [PrevMember](../mdx/prevmember-mdx.md) função. `Lag(-1)` é equivalente a [NextMember](../mdx/nextmember-mdx.md) função.  
  
 O **latência** função é semelhante ao [levar](../mdx/lead-mdx.md) funcionar, exceto que o **levar** função procura na direção oposta a **latência** função. Ou seja, `Lag(n)` é equivalente a `Lead(-n)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor para dezembro de 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o valor para março de 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
