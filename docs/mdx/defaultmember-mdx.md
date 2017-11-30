---
title: DefaultMember (MDX) | Microsoft Docs
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
f1_keywords: DefaultMember
dev_langs: kbMDX
helpviewer_keywords: DefaultMember function
ms.assetid: c1b53b3a-6e73-4c41-a4fe-9f5c96da5463
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f50284923b5df2765717a882bc9676f77e922e0c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o membro padrão de uma hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 O membro padrão em um atributo é usado para avaliar as expressões quando um atributo não for incluído em uma consulta.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa o **DefaultMember** função, em conjunto com o **nome** função para retornar o membro padrão para a dimensão de moeda de destino no cubo Adventure Works. O exemplo retorna **dólar americano**. O **nome** função é usada para retornar o nome da medida em vez da propriedade padrão de medida, que é **valor**.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [Definir um membro padrão](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
