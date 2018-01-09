---
title: IsGeneration (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ISGENERATION
dev_langs: kbMDX
helpviewer_keywords: IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d1b73679fed735599104dd3588d298602e48d3e7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
