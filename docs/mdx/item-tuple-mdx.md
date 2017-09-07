---
title: Item (tupla) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 9ee7af55-d5b5-47c8-a480-ef23878306af
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6e9411f3e4404a29ff0908ff53b0e0fb443b1703
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="item-tuple-mdx"></a>Item (Tupla) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma tupla de um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *String_Expression1*  
 Uma expressão de cadeia de caracteres válida que normalmente é uma tupla expressa em uma cadeia de caracteres.  
  
 *String_Expression2*  
 Uma expressão de cadeia de caracteres válida que normalmente é uma tupla expressa em uma cadeia de caracteres.  
  
 *Índice*  
 Uma expressão numérica válida que especifica a tupla específica através da posição dentro do conjunto a ser retornado.  
  
## <a name="remarks"></a>Comentários  
 O **Item** função retorna uma tupla do conjunto especificado. Há três maneiras possíveis de chamar o **Item** função:  
  
-   Se uma expressão única cadeia de caracteres for especificada, o **Item** função retorna a tupla especificada. Por exemplo, “([2005] .Q3, [Store05])”.  
  
-   Se mais de uma expressão de cadeia de caracteres for especificada, o **Item** função retorna a tupla definida pelas coordenadas especificadas. O número de cadeias de caracteres deve corresponder ao número de eixos e cada cadeia de caracteres deve identificar uma hierarquia exclusiva. Por exemplo, “[2005].Q3”, “[Store05]”.  
  
-   Se um inteiro for especificado, o **Item** função retorna a tupla que está na posição baseada em zero especificada por *índice*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna ([1996],Vendas):  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 O exemplo a seguir usa uma expressão de nível e retorna o Valor de Vendas pela Internet para cada Estado-Província da Austrália e seu percentual do Valor de Vendas pala Internet para a Austrália. Este exemplo usa a função Item para extrair a primeira (e apenas a tupla) do conjunto retornado pelo **ancestrais** função.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

