---
title: OpeningPeriod (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OPENINGPERIOD
dev_langs: kbMDX
helpviewer_keywords: OpeningPeriod function
ms.assetid: bebf55cf-e5c6-42b1-98f2-1d6e54093d4c
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8c9a23a96e24e454419b5ebf5c05663f188a8766
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 Essa função foi projetada para ser usada principalmente com a dimensão Tempo, mas pode ser usada com qualquer outra dimensão.  
  
-   Se uma expressão de nível for especificada, o **OpeningPeriod** função usa a hierarquia que contém o nível especificado e retorna o primeiro irmão entre os descendentes do membro padrão no nível especificado.  
  
-   Se uma expressão de nível e uma expressão de membro for especificados, o **OpeningPeriod** função retorna o primeiro irmão entre os descendentes do membro especificado no nível especificado na hierarquia que contém o nível especificado.  
  
-   Se nem uma expressão de nível nem uma expressão de membro for especificada, o **OpeningPeriod** função usa o nível padrão e o membro da dimensão com um tipo de tempo.  
  
> [!NOTE]  
>  O [ClosingPeriod](../mdx/closingperiod-mdx.md) função é semelhante ao **OpeningPeriod** funcionar, exceto que o **ClosingPeriod** função retorna o último irmão em vez do primeiro.  
  
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
 [TopCount &#40; MDX &#41;](../mdx/topcount-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40; MDX &#41;](../mdx/firstsibling-mdx.md)  
  
  
