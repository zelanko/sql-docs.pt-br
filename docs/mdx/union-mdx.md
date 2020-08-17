---
description: União (MDX)
title: União (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b0b4240d6c646761c5d962e4b9fa1ca54e0dcc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341202"
---
# <a name="union--mdx"></a>União (MDX)


  Retorna um conjunto gerado pela união de dois conjuntos, retendo membros duplicados opcionalmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>Argumentos  
 *Definir expressão 1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Definir expressão 2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 Essa função retorna a União de dois ou mais conjuntos especificados. Com a sintaxe padrão e com a sintaxe alternativa 1, as duplicatas são eliminadas por padrão. Com a sintaxe padrão, o uso do sinalizador **All** mantém duplicatas no conjunto Unido. As duplicatas são excluídas do final do conjunto. Com a sintaxe alternativa 2, as duplicatas são sempre retidas.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o comportamento da função **Union** usando cada sintaxe.  
  
### <a name="standard-syntax-duplicates-eliminated"></a>Sintaxe padrão, duplicatas eliminadas  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>Sintaxe padrão, duplicatas retidas  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>Sintaxe alternativa 1, duplicatas eliminadas  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>Sintaxe alternativa 2, duplicatas retidas  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [+ &#40;União&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
