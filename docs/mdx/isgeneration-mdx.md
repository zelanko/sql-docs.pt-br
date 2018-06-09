---
title: IsGeneration (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a726470f89f2d3ea1677259e849735a09909a42d
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740075"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)


  Retorna se um membro especificado estiver em uma geração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Generation_Number*  
 Uma expressão numérica válida que especifica a geração contra a qual o membro especificado é avaliado.  
  
## <a name="remarks"></a>Remarks  
 O **IsGeneration** função retorna **true** se o membro especificado é o número de geração especificado. Caso contrário, a função retorna **false**. Além disso, se o membro especificado for avaliada como um membro vazio, o **IsGeneration** função retorna **false**.  
  
 Com a finalidade de indexação de geração, os membros folha têm índice de geração 0. O índice de geração de membros não folha é determinado primeiro por obter o índice de geração mais alto a partir da união de todos os membros filho do membro especificado, adicionando 1 a esse índice. Devido à maneira como o índice de geração de membros não folha é determinado, um membro não folha específico pode pertencer a mais de uma geração.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna TRUE se [Date].[Fiscal].CurrentMember fizer parte da segunda geração:  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
