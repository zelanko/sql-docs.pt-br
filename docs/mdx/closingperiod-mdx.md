---
description: ClosingPeriod (MDX)
title: ClosingPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f457a941c8967ce6f3c6700760ff95d5c2999d0f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487629"
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)


  Retorna o membro que é o último irmão entre os descendentes de um membro especificado em um nível especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Essa função foi projetada para ser usada principalmente em uma dimensão com o tipo Tempo, mas também pode ser usada com qualquer outra dimensão.  
  
-   Se uma expressão de nível for especificada, a função **ClosingPeriod** usará a dimensão que contém o nível especificado e retornará o último irmão entre os descendentes do membro padrão no nível especificado.  
  
-   Se uma expressão de nível e uma expressão de membro forem especificadas, a função **ClosingPeriod** retornará o último irmão entre os descendentes do membro especificado no nível especificado.  
  
-   Se nenhuma expressão de nível nem uma expressão de membro for especificada, a função **ClosingPeriod** usará o nível padrão e o membro da dimensão (se houver) no cubo com um tipo de tempo.  
  
 A função **ClosingPeriod** é equivalente à seguinte instrução MDX:  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  A função [OpeningPeriod](../mdx/openingperiod-mdx.md) é semelhante à função **ClosingPeriod** , exceto que a função **OpeningPeriod** retorna o primeiro irmão em vez do último irmão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o valor da medida padrão para o membro Ano fiscal 2007 da dimensão Data (que possui o tipo semântico Tempo). Esse membro é retornado porque o nível Ano fiscal é o primeiro descendente do nível [All], a hierarquia Ano fiscal é a hierarquia padrão porque é a primeira hierarquia definida pelo usuário na coleção de hierarquias e o membro Ano fiscal 2007 é o último irmão dessa hierarquia nesse nível.  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna o valor da medida padrão para 30 de novembro de 2006 no nível Date.Date.Date da hierarquia de atributos Date.Date. Esse membro é o último irmão do descendente do nível [All] na hierarquia de atributos Date.Date.  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna o valor da medida padrão do membro Dezembro de 2003, que é o último irmão do descendente do membro 2003 no nível ano na hierarquia definida pelo usuário Calendário.  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna o valor da medida padrão do membro Junho de 2003, que é o último irmão do descendente do membro 2003 no nível ano na hierarquia definida pelo usuário Ano fiscal.  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OpeningPeriod&#41;MDX &#40;](../mdx/openingperiod-mdx.md)   
 [Referência de função MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling&#41;MDX &#40;](../mdx/lastsibling-mdx.md)  
  
  
