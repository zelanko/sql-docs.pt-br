---
description: Usando expressões de cubo e subcubo
title: Usando expressões de cubo e subcubo | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b431d82f24e5bf531dfa407d459ff9f36b543160
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341122"
---
# <a name="using-cube-and-subcube-expressions"></a>Usando expressões de cubo e subcubo


  As expressões de cubo e subcubo são usadas em instruções de linguagem MDX para definir, manipular ou recuperar dados de um cubo ou subcubo.  
  
## <a name="cube-expressions"></a>Expressões de cubo  
 As expressões de cubo contêm um identificador de cubo ou a palavra-chave CURRENTCUBE e, portanto, só podem ser expressões simples. Muitas instruções MDX usam a palavra-chave CURRENTCUBE para identificar o contexto de cubo atual em vez de requerer um identificador de cubo.  
  
 Um identificador de cubo aparece como *CUBE_NAME* nas descrições de notação de BNF de instruções MDX.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [A consulta MDX básica &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query)   
 [Criando subcubos em MDX &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)   
 [Instrução CREATE SUBCUBO &#40;MDX&#41;](../mdx/mdx-data-definition-create-subcube.md)   
 [Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)   
 [Instrução SCOPE &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)  
  
  
