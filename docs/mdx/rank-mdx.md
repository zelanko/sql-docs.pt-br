---
title: "Classificação (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: RANK
dev_langs: kbMDX
helpviewer_keywords: Rank function [MDX]
ms.assetid: 3cea35ed-57c4-4b47-a736-cee00275509b
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a00e9bcab64b29170ba05e9fa651d849a51b91ec
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="rank-mdx"></a>Rank (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Comentários  
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
 [Ordem &#40; MDX &#41;](../mdx/order-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
