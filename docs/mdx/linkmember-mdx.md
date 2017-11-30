---
title: LinkMember (MDX) | Microsoft Docs
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
f1_keywords: LINKMEMBER
dev_langs: kbMDX
helpviewer_keywords: LinkMember function
ms.assetid: b9106f07-8ea2-4933-aed3-ee9c63acf7ac
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a6fafec6febad45fe226bb9b96abd8c1ad3bd6da
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o membro equivalente a um membro especificado em uma hierarquia especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 O **LinkMember** função retorna o membro da hierarquia especificada que corresponde aos valores de chave em cada nível do membro especificado em uma hierarquia relacionada. Os atributos em cada nível devem ter a mesma cardinalidade de chave e tipo de dados. Em hierarquias não naturais, se houver mais de uma correspondência para um valor de chave do atributo, o resultado será um erro ou indeterminado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o **LinkMember** função para retornar a medida padrão no cubo Adventure Works para os ascendentes do membro 1º de julho de 2002 da hierarquia de atributo Date na hierarquia de calendário.  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquize &#40; MDX &#41;](../mdx/hierarchize-mdx.md)   
 [Ascendentes &#40; MDX &#41;](../mdx/ascendants-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
