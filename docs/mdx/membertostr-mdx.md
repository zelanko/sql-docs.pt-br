---
title: MemberToStr=1=«membro»=retorna (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ff7ffb1b57c8af38e1b2eeebc64f2a3e753fc5b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278493"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


  Retorna uma cadeia de caracteres formatada para MDX que corresponde a um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Esta função retorna uma cadeia de caracteres que contém o nome exclusivo de um membro. Ele geralmente é usado para passar o nome exclusivo de um membro para uma função externa.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a cadeia de caracteres [Geography]. [Geography]. [Country]. & [United States]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
