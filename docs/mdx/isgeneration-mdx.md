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
ms.openlocfilehash: 401a11a10f190cda8efeaffa04e1025ef7f4e681
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68105231"
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
  
## <a name="remarks"></a>Comentários  
 A função **IsGeneration** retornará **true** se o membro especificado estiver no número de geração especificado. Caso contrário, a função retornará **false**. Além disso, se o membro especificado for avaliado como um membro vazio, a função **IsGeneration** retornará **false**.  
  
 Com a finalidade de indexação de geração, os membros folha têm índice de geração 0. O índice de geração de membros não folha é determinado primeiro por obter o índice de geração mais alto a partir da união de todos os membros filho do membro especificado, adicionando 1 a esse índice. Devido à maneira como o índice de geração de membros não folha é determinado, um membro não folha específico pode pertencer a mais de uma geração.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna TRUE se [Date].[Fiscal].CurrentMember fizer parte da segunda geração:  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
