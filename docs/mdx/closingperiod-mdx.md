---
title: ClosingPeriod (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CLOSINGPERIOD
dev_langs: kbMDX
helpviewer_keywords: ClosingPeriod function
ms.assetid: ae709017-219d-43e1-a98a-a85bd365b4cd
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: db1f3170f51d72f912dc84efce36eceeb9e839ec
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
-   Se uma expressão de nível for especificada, o **ClosingPeriod** função usa a dimensão que contém o nível especificado e retorna o último irmão entre os descendentes do membro padrão no nível especificado.  
  
-   Se uma expressão de nível e uma expressão de membro for especificados, o **ClosingPeriod** função retorna o último irmão entre os descendentes do membro especificado no nível especificado.  
  
-   Se nem uma expressão de nível nem uma expressão de membro for especificada, o **ClosingPeriod** função usa o nível padrão e o membro da dimensão (se houver) no cubo com um tipo de tempo.  
  
 O **ClosingPeriod** função é equivalente à instrução MDX a seguir:  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  O [OpeningPeriod](../mdx/openingperiod-mdx.md) função é semelhante ao **ClosingPeriod** funcionar, exceto que o **OpeningPeriod** função retorna o primeiro irmão em vez do último.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [OpeningPeriod &#40; MDX &#41;](../mdx/openingperiod-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40; MDX &#41;](../mdx/lastsibling-mdx.md)  
  
  
