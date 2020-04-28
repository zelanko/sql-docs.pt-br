---
title: Item (tupla) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5740095752b482430cd718d0e2bff813449d92ef
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68105217"
---
# <a name="item-tuple-mdx"></a>Item (Tupla) (MDX)


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
  
 *Index*  
 Uma expressão numérica válida que especifica a tupla específica através da posição dentro do conjunto a ser retornado.  
  
## <a name="remarks"></a>Comentários  
 A função **Item** retorna uma tupla do conjunto especificado. Há três maneiras possíveis de chamar a função **Item** :  
  
-   Se uma única expressão de cadeia de caracteres for especificada, a função **Item** retornará a tupla especificada. Por exemplo, “([2005] .Q3, [Store05])”.  
  
-   Se mais de uma expressão de cadeia de caracteres for especificada, a função **Item** retornará a tupla definida pelas coordenadas especificadas. O número de cadeias de caracteres deve corresponder ao número de eixos e cada cadeia de caracteres deve identificar uma hierarquia exclusiva. Por exemplo, “[2005].Q3”, “[Store05]”.  
  
-   Se um inteiro for especificado, a função **Item** retornará a tupla que está na posição baseada em zero especificada pelo *índice*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna ([1996],Vendas):  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 O exemplo a seguir usa uma expressão de nível e retorna o Valor de Vendas pela Internet para cada Estado-Província da Austrália e seu percentual do Valor de Vendas pala Internet para a Austrália. Este exemplo usa a função item para extrair a primeira (e somente tupla) do conjunto retornado pela função **ancestrais** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
