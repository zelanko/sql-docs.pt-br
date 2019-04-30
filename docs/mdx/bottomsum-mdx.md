---
title: BottomSum (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f923761144389a97962f7269cc5164d0dbdbf51
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306715"
---
# <a name="bottomsum-mdx"></a>BottomSum (MDX)


  Classifica um conjunto especificado em ordem crescente e retorna um conjunto de tuplas com os valores mais baixos, cuja soma é igual a ou menor que um valor especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BottomSum(Set_Expression, Value, Numeric_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Value*  
 Uma expressão numérica válida que especifica o valor contra o qual cada tupla é comparada.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 O **BottomSum** função calcula a soma de uma medida especificada avaliada sobre um conjunto especificado, classificando o conjunto em ordem crescente. Em seguida, a função retorna os elementos com os valores mais baixos, cujo total da expressão numérica especificada seja, pelo menos, o valor especificado (soma). Essa função retorna o subconjunto menor de um conjunto cujo total cumulativo é pelo menos o valor especificado. Os elementos retornados são classificados do menor para maior.  
  
> [!IMPORTANT]  
>  O **BottomSum** função, como o [TopSum](../mdx/topsum-mdx.md) de função, sempre quebra a hierarquia.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna, para a categoria Bicicleta, o menor conjunto de membros do nível Cidade na hierarquia Geografia, na dimensão Geografia, do ano fiscal de 2003, cujo total cumulativo que usa a medida Valor das Vendas do Revendedor é pelo menos a soma de 50.000 (começando com os membros desse conjunto com o menor número de vendas):  
  
 `SELECT`  
  
 `[Product].[Product Categories].Bikes ON 0,`  
  
 `BottomSum`  
  
 `({[Geography].[Geography].[City].Members}`  
  
 `, 50000`  
  
 `, ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)`  
  
 `) ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
