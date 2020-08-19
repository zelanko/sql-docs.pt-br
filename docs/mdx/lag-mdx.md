---
description: Latência (MDX)
title: Latência (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bc9beb8215d8d690f2d4ccdf43c3aaf03096b9d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477038"
---
# <a name="lag-mdx"></a>Latência (MDX)


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
  
## <a name="remarks"></a>Comentários  
 As posições de membros em um nível são determinadas pela ordem natural da hierarquia de atributo. A numeração das posições se baseia em zero.  
  
 Se o retardo especificado for zero, a função **lag** retornará o próprio membro especificado.  
  
 Se o retardo especificado for negativo, a função **lag** retornará um membro subsequente.  
  
 `Lag(1)` é equivalente à função [PrevMember](../mdx/prevmember-mdx.md) . `Lag(-1)` é equivalente à função [NextMember](../mdx/nextmember-mdx.md) .  
  
 A função **lag** é semelhante à função [Lead](../mdx/lead-mdx.md) , exceto que a função **Lead** procura na direção oposta à função **lag** . Ou seja, `Lag(n)` é equivalente a `Lead(-n)`.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
