---
description: OpeningPeriod (MDX)
title: OpeningPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ba59621ba52043dac56a9cfcae5ae1cb8b675f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471758"
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)


  Retorna o primeiro irmão entre os descendentes de um nível especificado, opcionalmente em um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Essa função foi projetada para ser usada principalmente com a dimensão Tempo, mas pode ser usada com qualquer outra dimensão.  
  
-   Se uma expressão de nível for especificada, a função **OpeningPeriod** usará a hierarquia que contém o nível especificado e retornará o primeiro irmão entre os descendentes do membro padrão no nível especificado.  
  
-   Se uma expressão de nível e uma expressão de membro forem especificadas, a função **OpeningPeriod** retornará o primeiro irmão entre os descendentes do membro especificado no nível especificado dentro da hierarquia que contém o nível especificado.  
  
-   Se nenhuma expressão de nível nem uma expressão de membro forem especificadas, a função **OpeningPeriod** usará o nível padrão e o membro da dimensão com um tipo de tempo.  
  
> [!NOTE]  
>  A função [ClosingPeriod](../mdx/closingperiod-mdx.md) é semelhante à função **OpeningPeriod** , exceto que a função **ClosingPeriod** retorna o último irmão em vez do primeiro irmão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o valor de medida padrão para o membro Ano fiscal 2002 da dimensão Data (que possui o tipo Tempo). Esse membro é retornado porque o nível Ano fiscal é o primeiro descendente do nível [All], a hierarquia Ano fiscal é a hierarquia padrão porque é a primeira hierarquia definida pelo usuário na coleção de hierarquias e o membro Ano fiscal 2002 é o primeiro irmão dessa hierarquia nesse nível.  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o valor da medida padrão para 1º de julho de 2001 no nível Date.Date.Date da hierarquia de atributos Date.Date. Esse membro é o primeiro irmão do descendente do nível [All] na hierarquia de atributos Date.Date.  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o valor da medida padrão do membro Janeiro de 2003, que é o primeiro irmão do descendente do membro 2003 no nível ano na hierarquia definida pelo usuário Calendário.  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o valor da medida padrão do membro Julho de 2002, que é o primeiro irmão do descendente do membro 2003 no nível ano na hierarquia definida pelo usuário Ano fiscal.  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [TopCount&#41;MDX &#40;](../mdx/topcount-mdx.md)   
 [Referência de função MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling&#41;MDX &#40;](../mdx/firstsibling-mdx.md)  
  
  
