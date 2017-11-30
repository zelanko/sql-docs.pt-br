---
title: "Latência (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LAG
dev_langs: kbMDX
helpviewer_keywords: Lag function
ms.assetid: 08c704ea-35d8-44ee-abe5-93bd24b99906
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 22d3e6c8abe087c6af7bbcca29ebb2ee9d8bedc0
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
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
  
## <a name="remarks"></a>Comentários  
 As posições de membros em um nível são determinadas pela ordem natural da hierarquia de atributo. A numeração das posições se baseia em zero.  
  
 Se o retardo especificado for zero, o **latência** função retorna o próprio membro especificado.  
  
 Se o retardo especificado for negativo, o **latência** função retorna um membro subsequente.  
  
 `Lag(1)`é equivalente a [PrevMember](../mdx/prevmember-mdx.md) função. `Lag(-1)`é equivalente a [NextMember](../mdx/nextmember-mdx.md) função.  
  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
