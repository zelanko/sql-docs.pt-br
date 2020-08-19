---
description: NonEmpty (MDX)
title: Não vazio (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b887988327908f128633349de52f39a17d1e0978
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483719"
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)


  Retorna o conjunto de tuplas que não estão vazias a partir de um conjunto especificado, com base no produto cruzado do conjunto especificado com um segundo conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>Argumentos  
 *set_expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *set_expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 Essa função retorna as tuplas do primeiro conjunto especificado que não estão vazias, quando avaliadas pelas tuplas do segundo conjunto. A função não **vazia** leva em conta cálculos e preserva tuplas duplicadas. Se um segundo conjunto não for fornecido, a expressão será avaliada no contexto das coordenadas atuais dos membros das hierarquias de atributos e medidas no cubo.  
  
> [!NOTE]  
>  Use essa função em vez do NonEmptyCrossjoin preterido [&#40;função&#41;MDX ](../mdx/nonemptycrossjoin-mdx.md) .  
  
> [!IMPORTANT]  
>  Não vazia é uma característica das referências de células pelas tuplas, não as próprias tuplas.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra um exemplo simples de não **vazio**, retornando todos os clientes que tinham um valor não nulo para o valor de vendas pela Internet em 1º de julho de 2001:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 O exemplo a seguir retorna o conjunto de tuplas que contém clientes e datas de compra, usando a função de **filtro** e as funções não **vazias** para localizar a última data em que cada cliente fez uma compra:  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;MDX do DefaultMember &#40;](../mdx/defaultmember-mdx.md)   
 [Filtrar &#40;&#41;MDX ](../mdx/filter-mdx.md)   
 [IsEmpty &#40;&#41;MDX ](../mdx/isempty-mdx.md)   
 [Referência de função MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin&#41;MDX &#40;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
