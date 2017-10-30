---
title: IsGeneration (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISGENERATION
dev_langs:
- kbMDX
helpviewer_keywords:
- IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bdb02d424cb58aab2e8af8695b9751e495ba7175
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

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
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

