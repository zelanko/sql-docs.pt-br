---
title: "Usando funções de cadeia de caracteres | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- string functions
ms.assetid: 962e820a-a1f9-49b5-90f0-a05261e6682b
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 12fc2dca6c7a0eb1c7d126ef0cfdc87df869c878
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="using-string-functions"></a>Usando as funções de cadeia de caracteres
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Você pode usar as funções de cadeia de caracteres em praticamente todos os objetos em Multidimensional Expressions (MDX). Em procedimentos armazenados, use as funções de cadeia de caracteres principalmente para converter o objeto em uma representação de cadeia de caracteres. Também é possível usar as funções de cadeia de caracteres para avaliar uma expressão de cadeia de caracteres sobre um objeto para retornar um valor.  
  
 As funções de cadeia de caracteres mais amplamente utilizadas são **nome** e **Uniquename**. Respectivamente, estas funções retornam o nome e o nome exclusivo de um objeto. Elas são usadas principalmente ao depurar cálculos para identificar qual membro está sendo retornando por uma função.  
  
## <a name="examples"></a>Exemplos  
 As consultas de exemplo a seguir mostram como usar estas funções:  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 O **gerar** função pode ser usada para executar uma função de cadeia de caracteres em todos os membros de um conjunto e concatenar os resultados. Isto também pode ser útil ao depurar cálculos, pois permite visualizar o conteúdo de um conjunto. O exemplo a seguir mostra como usá-la desse modo:  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Outro grupo de funções de cadeia de caracteres usadas com frequência são as que permitem converter uma cadeia de caracteres que contém o nome exclusivo de um objeto ou uma expressão que resolve o objeto no próprio objeto. A consulta de exemplo a seguir demonstra como o **StrToMember** e **StrToSet** funções fazer isso:  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  O **StrToMember** e **StrToSet** funções devem ser usadas com cuidado. Elas podem gerar um desempenho de consulta insatisfatório se forem usadas em definições de cálculo.  
  
## <a name="see-also"></a>Consulte também  
 [Gerar &#40; MDX &#41;](../mdx/generate-mdx.md)   
 [Nome &#40; MDX &#41;](../mdx/name-mdx.md)   
 [UniqueName &#40; MDX &#41;](../mdx/uniquename-mdx.md)   
 [Funções &#40; Sintaxe MDX &#41;](../mdx/functions-mdx-syntax.md)   
 [Usando procedimentos armazenados &#40; MDX &#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40; MDX &#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40; MDX &#41;](../mdx/strtoset-mdx.md)  
  
  

