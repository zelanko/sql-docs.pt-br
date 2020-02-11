---
title: Dimensão (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 58bee93a4cef37a8a5a71211b292a16392687f12
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67999954"
---
# <a name="dimension-mdx"></a>Função Dimension (MDX)


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
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
### <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a função de **dimensão** , em conjunto com a função **Name** , para retornar o nome da hierarquia do membro especificado.  
  
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
  
 O exemplo a seguir usa a função de **dimensão** , em conjunto com os **Membros** e as funções de **contagem** , para retornar o número de membros na hierarquia que contém o membro especificado.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Contar &#40;níveis de hierarquia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Contagem &#40;definida&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Níveis &#40;&#41;MDX](../mdx/levels-mdx.md)   
 [Membros &#40;definidos&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)   
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
