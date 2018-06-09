---
title: Classificação (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1d234f02c8dfcd36073059210c1999cb95f5ab0
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742725"
---
# <a name="rank-mdx"></a>Rank (MDX)


  Retorna a classificação de base um de uma tupla especificada em um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Remarks  
 Se uma expressão numérica for especificada, o **classificação** função determina a classificação baseada em um para a tupla especificada, avaliando a expressão numérica especificada em relação à tupla. Se uma expressão numérica for especificada, o **classificação** função atribui a mesma classificação a tuplas com valores duplicados no conjunto. Essa atribuição da mesma classificação para valores duplicados afeta as classificações de tuplas subsequentes no conjunto. Por exemplo, um conjunto é formado pelas seguintes tuplas, `{(a,b), (e,f), (c,d)}`. A tupla `(a,b)` tem o mesmo valor que a tupla `(c,d)`. Se a tupla `(a,b)` tiver uma classificação 1, então tanto `(a,b)` quanto `(c,d)` terão uma classificação 1. No entanto, a tupla `(e,f)` teria uma classificação 3. Não poderia haver uma tupla com classificação 2 nesse conjunto.   
  
 Se uma expressão numérica não for especificada, o **classificação** função retorna a posição ordinal baseada em um da tupla especificada.  
  
 O **classificação** função não ordena o conjunto.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o conjunto de tuplas contendo clientes e datas de compra, usando o **filtro**, **NonEmpty**, **Item**, e **classificação** funções para localizar a última data em que uma compra feita pelo cliente.  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir usa o **ordem** função, em vez de **classificação** função, para classificar os membros da hierarquia cidade com base na medida do valor de vendas de revendedor e, em seguida, exibe-os na ordem de classificação. Usando o **ordem** funcionar para organizar pela primeira vez o conjunto de membros da hierarquia cidade, a classificação é feita apenas uma vez e, em seguida, seguida por uma verificação linear antes de ser apresentada na ordem de classificação.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Ordem &#40;MDX&#41;](../mdx/order-mdx.md)   
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
