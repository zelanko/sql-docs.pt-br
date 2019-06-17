---
title: BottomPercent (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a627ea8e5dd7a8f8266fcf0ea374e6abcde4bdc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208793"
---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)


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
  
## <a name="remarks"></a>Comentários  
 O **BottomPercent** função calcula a soma da expressão numérica especificada avaliada sobre um conjunto especificado, classificando o conjunto em ordem crescente. A função retorna os elementos com os valores mais baixos, cujo percentual cumulativo do valor total somado seja pelo menos o percentual especificado. Essa função retorna o subconjunto menor de um conjunto cujo total cumulativo é pelo menos o percentual especificado. Os elementos retornados são classificados do maior para menor.  
  
> [!IMPORTANT]  
>  O **BottomPercent** função, como o [TopPercent](../mdx/toppercent-mdx.md) de função, sempre quebra a hierarquia. Para obter mais informações, consulte Função Order.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
