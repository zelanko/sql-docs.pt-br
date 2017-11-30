---
title: "Usando o cubo e subcubo expressões | Microsoft Docs"
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
dev_langs: kbMDX
helpviewer_keywords:
- subcubes [MDX]
- cubes [Analysis Services], MDX
- CURRENTCUBE keyword
- expressions [MDX], subcubes
- expressions [MDX], cubes
ms.assetid: 95ae034d-8f88-4820-91c6-205ec424e119
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e8e4ee0d95aa58acb6c26c325b31303059b19818
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="using-cube-and-subcube-expressions"></a>Usando expressões de cubo e subcubo
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  As expressões de cubo e subcubo são usadas em instruções de linguagem MDX para definir, manipular ou recuperar dados de um cubo ou subcubo.  
  
## <a name="cube-expressions"></a>Expressões de cubo  
 As expressões de cubo contêm um identificador de cubo ou a palavra-chave CURRENTCUBE e, portanto, só podem ser expressões simples. Muitas instruções MDX usam a palavra-chave CURRENTCUBE para identificar o contexto de cubo atual em vez de requerer um identificador de cubo.  
  
 Um identificador de cubo aparece como *Cube_Name* nas descrições de notação BNF de instruções MDX.  
  
 As expressões de cubo podem aparecer em vários locais. Em uma instrução SELECT MDX, elas especificam o cubo do qual dados serão recuperados. Na consulta de exemplo a seguir, a expressão [Adventure Works] refere-se ao cubo com esse nome:  
  
 `SELECT [Measures].[Internet Sales Amount] ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 Na instrução CREATE MEMBER, a expressão de cubo especifica em qual cubo o membro calculado que está sendo criado irá aparecer. No exemplo a seguir, a instrução cria uma medida calculada na dimensão Medidas do cubo Adventure Works:  
  
 `CREATE MEMBER [Adventure Works].[Measures].[Test] AS 1`  
  
 Ao usar a instrução CREATE MEMBER em um script MDX, o nome do cubo pode ser substituído pela palavra-chave CURRENTCUBE, visto que o cubo onde o membro calculado deve ser criado será o mesmo cubo ao qual o script MDX pertence, como mostra o exemplo a seguir:  
  
 `CREATE MEMBER CURRENTCUBE.[Measures].[Test] AS 1;`  
  
 Fazer isso facilita copiar e colar definições de membro calculado de um cubo para outro, pois o nome do cubo não é mais codificado.  
  
## <a name="subcube-expressions"></a>Expressões de subcubo  
 Uma expressão de subcubo pode conter um identificador de subcubo ou uma instrução MDX que retorna um subcubo. Se contiver um identificador de subcubo, a expressão de subcubo será uma expressão simples. Se contiver uma instrução MDX que retorna um subcubo, a expressão de subcubo será uma instrução complexa. Por exemplo, a instrução SELECT MDX retorna um subcubo e é usada onde expressões de subcubo são permitidas, como mostra o exemplo a seguir:  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Date].[Calendar Year].MEMBERS ON ROWS`  
  
 `FROM`  
  
 `(SELECT [Measures].[Internet Sales Amount] ON COLUMNS,`  
  
 `[Date].[Calendar Year].&[2004] ON ROWS`  
  
 `FROM [Adventure Works])`  
  
 Este uso de uma instrução SELECT na cláusula FROM também é mencionado como uma subseleção.  
  
 Outro cenário comum onde são encontradas expressões de subcubo apresenta-se ao fazer atribuições de escopo em um script MDX. No exemplo a seguir, a instrução SCOPE é usada para limitar uma atribuição a um subcubo que consiste em [Medidas]. [Quantidade de Vendas pela Internet]:  
  
 `SCOPE([Measures].[Internet Sales Amount]);`  
  
 `This=1;`  
  
 `END SCOPE;`  
  
 Um identificador de subcubo aparece como *Subcube_Name*. em descrições de notação BNF de instruções MDX.  
  
## <a name="see-also"></a>Consulte também  
 [A consulta MDX básica &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [Criando subcubos em MDX &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md)   
 [Criar SUBCUBO instrução &#40; MDX &#41;](../mdx/mdx-data-definition-create-subcube.md)   
 [Expressões &#40; MDX &#41;](../mdx/expressions-mdx.md)   
 [Instrução SCOPE &#40; MDX &#41;](../mdx/mdx-scripting-scope.md)  
  
  
