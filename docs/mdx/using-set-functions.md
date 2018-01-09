---
title: "Usando funções de conjunto | Microsoft Docs"
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
dev_langs: kbMDX
helpviewer_keywords: set functions [MDX]
ms.assetid: b08ddc9d-38f8-41aa-b791-b5352f1a8783
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c0afa99103cbb10c29c66bc375dc10d206560fd8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="using-set-functions"></a>Usando funções de conjunto
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Uma função de conjunto recupera um conjunto de uma dimensão, hierarquia, nível ou por meio do desvio dos locais absolutos e relativos dos membros nesses objetos, criando conjuntos de várias maneiras.  
  
 As funções de conjunto, assim como as funções de membro e de tupla, são essenciais para negociar as estruturas multidimensionais encontradas no Analysis Services. As funções de conjunto também são essenciais para obter resultados a partir de consultas MDX uma vez que as expressões de conjunto definem os eixos de uma consulta MDX.  
  
 Uma das funções de conjunto mais comuns é o [membros &#40; Definir &#41; &#40; MDX &#41; ](../mdx/members-set-mdx.md) função, que recupera um conjunto contendo todos os membros de dimensão, hierarquia ou nível. O seguinte é um exemplo de seu uso em uma consulta:  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Outra função geralmente usada é a [Crossjoin &#40; MDX &#41; ](../mdx/crossjoin-mdx.md) função. Ela retorna um conjunto de tuplas que representam o produto cartesiano dos conjuntos transmitidos como parâmetros. Em termos práticos, esta função permite criar eixos “aninhados” ou “de referência cruzada” em consultas:  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 O [descendentes &#40; MDX &#41; ](../mdx/descendants-mdx.md) função é semelhante a **filhos** funcionarão, mas é mais eficiente. Ela retorna os descendentes de qualquer membro em um ou mais níveis em uma hierarquia:  
  
 SELECT  
  
 [Medidas].[Valor das Vendas pela Internet]  
  
 Colunas ON,  
  
 //Retorna um conjunto que contém todas as Datas abaixo do Ano Civil  
  
 //2004 na hierarquia Calendário da dimensão Data  
  
 DESCENDANTS(  
  
 [Data]. [Calendário]. [Ano calendário]. & [2004]  
  
 , [Data].[Calendário].[Data])  
  
 Linhas ON  
  
 FROM [Adventure Works]  
  
 O [ordem &#40; MDX &#41; ](../mdx/order-mdx.md) função permite organizar o conteúdo de um conjunto em ordem de acordo com uma expressão numérica específica crescente ou decrescente. A consulta a seguir retorna os mesmos membros das linhas como a consulta anterior, mas agora os ordena pela medida Quantidade de Vendas pela Internet:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Esta consulta também ilustra como o conjunto retornado de uma função de conjunto, Descendants, pode ser transmitido como um parâmetro a outra função de conjunto, Order.  
  
 Um conjunto de acordo com determinados critérios de filtragem é muito útil ao escrever consultas e para essa finalidade, você pode usar o [filtro &#40; MDX &#41; ](../mdx/filter-mdx.md) de função, conforme mostrado no exemplo a seguir:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Existem outras funções mais sofisticadas que permitem filtrar um conjunto de outros modos. Por exemplo, a consulta a seguir mostra o [TopCount &#40; MDX &#41; ](../mdx/topcount-mdx.md) função retorna os n primeiros itens em um conjunto:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Finalmente, é possível executar várias operações de conjunto lógicas usando funções como [Intersect &#40; MDX &#41; ](../mdx/intersect-mdx.md), [União &#40; MDX &#41; ](../mdx/union-mdx.md) e [exceto &#40; MDX &#41; ](../mdx/except-mdx-function.md) funções. A consulta a seguir mostra exemplos das duas últimas funções:  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40; Sintaxe MDX &#41;](../mdx/functions-mdx-syntax.md)   
 [Usando funções de membro](../mdx/using-member-functions.md)   
 [Usando funções de tupla](../mdx/using-tuple-functions.md)  
  
  
