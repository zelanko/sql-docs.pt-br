---
title: BottomSum (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BOTTOMSUM
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomSum function
ms.assetid: b3b10e68-2a36-4c38-85f4-3bb7917d5ae8
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: f2080c608bc80f9d86f9b74e3ba2deebff8f837d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bottomsum-mdx"></a>BottomSum (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 O **BottomSum** função calcula a soma de uma medida especificada avaliada em um conjunto especificado, classificando o conjunto em ordem crescente. Em seguida, a função retorna os elementos com os valores mais baixos, cujo total da expressão numérica especificada seja, pelo menos, o valor especificado (soma). Essa função retorna o subconjunto menor de um conjunto cujo total cumulativo é pelo menos o valor especificado. Os elementos retornados são classificados do menor para maior.  
  
> [!IMPORTANT]  
>  O **BottomSum** função, como o [TopSum](../mdx/topsum-mdx.md) funcionar, sempre quebra a hierarquia.  
  
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
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
