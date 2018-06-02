---
title: Dimensão (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: af73d6f08432a63a207c06d361354d6e45b6a07d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577928"
---
# <a name="dimension-mdx"></a>Função Dimension (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a hierarquia que contém um membro, nível ou hierarquia especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.Dimension  
  
Level syntax  
Level_Expression.Dimension  
  
Member syntax  
Member_Expression.Dimension  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
### <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o **dimensão** função, em conjunto com o **nome** função para retornar o nome da hierarquia do membro especificado.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Name  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir usa a função Dimension, junto com as funções Levels e Count, para retornar o número de níveis da hierarquia que contém o membro especificado.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir usa o **dimensão** função, em conjunto com o **membros** e **contagem** funções para retornar o número de membros na hierarquia que contém o membro especificado.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Contagem de &#40;níveis de hierarquia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Contagem de &#40;definir&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Níveis &#40;MDX&#41;](../mdx/levels-mdx.md)   
 [Membros &#40;definir&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)   
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
