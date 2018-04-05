---
title: BottomPercent (MDX) | Microsoft Docs
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
- BOTTOMPERCENT
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomPercent function
ms.assetid: c04866e6-e6dd-4ed1-ae79-c718c194930c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 078221baa088e0375af381e1e4ef5579280a2cb3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Classifica um conjunto em ordem crescente e retorna um conjunto de tuplas com os valores mais baixos, cujo total cumulativo é igual ou maior do que um percentual especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Porcentagem*  
 Uma expressão numérica válida que especifica o percentual de tuplas a ser retornado.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Remarks  
 O **BottomPercent** função calcula a soma da expressão numérica especificada avaliada em um conjunto especificado, classificando o conjunto em ordem crescente. A função retorna os elementos com os valores mais baixos, cujo percentual cumulativo do valor total somado seja pelo menos o percentual especificado. Essa função retorna o subconjunto menor de um conjunto cujo total cumulativo é pelo menos o percentual especificado. Os elementos retornados são classificados do maior para menor.  
  
> [!IMPORTANT]  
>  O **BottomPercent** função, como o [TopPercent](../mdx/toppercent-mdx.md) funcionar, sempre quebra a hierarquia. Para obter mais informações, consulte Função Order.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna, para a categoria Bicicleta, o menor conjunto de membros do nível Cidade na hierarquia Geografia, na dimensão Geografia, do ano fiscal de 2003, cujo total cumulativo que usa a medida Valor das Vendas do Revendedor é pelo menos 15% do total cumulativo (começando com os membros desse conjunto com o menor número de vendas).  
  
```  
SELECT  
[Product].[Product Categories].Bikes ON 0,  
BottomPercent  
   ({[Geography].[Geography].[City].Members}  
   , 15  
   , ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)  
   ) ON 1  
FROM [Adventure Works]  
WHERE ([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
