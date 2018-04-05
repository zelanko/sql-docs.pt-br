---
title: Usando expressões de membros | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- members [MDX], expressions
- expressions [MDX], members
ms.assetid: 63c7af49-8bea-47c5-9566-a961f77d2a3d
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bc1574fc06eeaa032fb68d395106721fc33ec699
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="using-member-expressions"></a>Usando expressões de membros
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Uma expressão de membro contém um identificador, uma função ou uma expressão que pode ser convertida em um membro.  
  
 Identificadores de membro podem vir em muitos formatos diferentes. A forma mais simples de um identificador de membro consiste no nome do membro. Por exemplo:  
  
```  
SELECT Amount ON 0  
FROM [Adventure Works]  
  
```  
  
 No entanto, se houver vários membros com o mesmo nome em hierarquias diferentes, não há nenhum método para determinar qual membro será retornado pela consulta. Por exemplo, a consulta a seguir solicita dados para um membro com o nome [CY 2004]. A consulta é executada com êxito, mas há pelo menos seis membros com esse nome no cubo Adventure Works:  
  
```  
SELECT [CY 2004] ON 0  
FROM [Adventure Works]  
  
```  
  
 Desse modo, a forma mais confiável do identificador de membro é o nome exclusivo do membro, que permite identificar um membro específico em um cubo. O Analysis Services pode gerar nomes exclusivos de diversos modos, mas um nome exclusivo sempre é composto de pelo menos dois identificadores: o nome da dimensão e o nome ou a chave do membro. Um nome exclusivo aparece no seguinte formato:  
  
```  
  
Dimension_Name  
.[Hierarchy_Name.] [[{Member_Name | &Member_Key}.]... ] {Member_Name | &Member_Key}  
  
```  
  
 Veja alguns exemplos de nomes exclusivos de membro do cubo Adventure Works:  
  
```  
[Measures].[Amount]  
[Date].[Calendar Year].&[2004]  
[Date].[Calendar].[Calendar Quarter].&[2004]&[1]  
[Employee].[Employees].&[112]  
[Product].[Product Categories].[All Products]  
  
```  
  
 Existem muitas funções MDX que retornam membros. Para obter uma lista completa, consulte [referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  Para obter mais informações sobre nomes de membros e as chaves de membro, consulte [trabalhando com membros, tuplas e conjuntos de &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40; MDX &#41;](../mdx/expressions-mdx.md)  
  
  
