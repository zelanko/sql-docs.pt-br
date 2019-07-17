---
title: IsSibling (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 15c80cec67b0a40c8ac4c436a45a4551132858f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105355"
---
# <a name="issibling-mdx"></a>IsSibling (MDX)


  Retorna se um membro especificado for um irmão de outro membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression1*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Member_Expression2*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 O **IsSibling** retornos de função **verdadeiro** se o primeiro membro especificado for um irmão do segundo membro especificado. Caso contrário, a função retornará **falsos**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retornará TRUE se o membro atual da hierarquia Fiscal da dimensão Data for um irmão de julho de 2002:  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
