---
title: DISTINCT (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 628a175ea1c7b89b2352c34449ba40eb1d0ea1e2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579298"
---
# <a name="distinct-mdx"></a>Distinct (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Avalia um conjunto especificado, remove tuplas duplicadas do conjunto e retorna o conjunto resultante.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Distinct(Set_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Remarks  
 Se o **Distinct** função encontra tuplas duplicadas no conjunto especificado, a função manterá apenas a primeira instância da tupla duplicada, deixando a ordem do conjunto intacta.  
  
## <a name="examples"></a>Exemplos  
 A consulta de exemplo a seguir mostra como usar a função Distinct com um conjunto nomeado, bem como usá-la com a função Count para localizar o número de tuplas distintas em um conjunto:  
  
 `WITH SET MySet AS`  
  
 `{[Customer].[Customer Geography].[Country].&[Australia],[Customer].[Customer Geography].[Country].&[Australia],`  
  
 `[Customer].[Customer Geography].[Country].&[Canada],[Customer].[Customer Geography].[Country].&[France],`  
  
 `[Customer].[Customer Geography].[Country].&[United Kingdom],[Customer].[Customer Geography].[Country].&[United Kingdom]}`  
  
 `MEMBER MEASURES.SETCOUNT AS`  
  
 `COUNT(MySet)`  
  
 `MEMBER MEASURES.SETDISTINCTCOUNT AS`  
  
 `COUNT(DISTINCT(MySet))`  
  
 `SELECT {MEASURES.SETCOUNT, MEASURES.SETDISTINCTCOUNT} ON 0,`  
  
 `DISTINCT(MySet) ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
