---
title: MemberToStr (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac9998edcf11477a2a4aff1af951d2dc4a17cbbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581568"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna uma cadeia de caracteres formatada em linguagem MDX que corresponde a um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 Esta função retorna uma cadeia de caracteres que contém o nome exclusivo de um membro. Ele é normalmente usado para passar o nome exclusivo de um membro para uma função externa.  
  
## <a name="example"></a>Exemplo  
 O exemplo seguinte retorna a cadeia de caracteres [Geography].[Geography].[Country].&[United States]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
