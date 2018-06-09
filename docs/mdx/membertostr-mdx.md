---
title: MemberToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9bd0b59cca8560ae615e7044f13161a01f26835b
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742095"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


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
  
  
