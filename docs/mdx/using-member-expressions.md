---
description: Usando expressões de membros
title: Usando expressões de membro | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e833d8d579841a3fc15aad89612a1d25b71fd0f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494819"
---
# <a name="using-member-expressions"></a>Usando expressões de membros


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
  
 Existem muitas funções MDX que retornam membros. Para obter uma lista completa, consulte [referência de função mdx &#40;mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  Para obter mais informações sobre nomes de membros e chaves de membro, consulte [trabalhando com membros, tuplas e conjuntos &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx).  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
