---
title: Intersect (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f253dad526c509edff5c837b61ae2faae07d5758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68105366"
---
# <a name="intersect-mdx"></a>Função Intersect (MDX)


  Retorna a interseção de dois conjuntos de entrada, mantendo as duplicatas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 A função **Intersect** retorna a interseção de dois conjuntos. Por padrão, a função remove as duplicações antes de interseccionar os dois conjuntos. Os dois conjuntos devem ter a mesma dimensionalidade.  
  
 O sinalizador **All** opcional retém duplicatas. Se **All** for especificado, a função **Intersect** interseccionará elementos não duplicados como de costume e também interseccionará cada duplicata no primeiro conjunto que tem uma duplicata correspondente no segundo conjunto. Os dois conjuntos devem ter a mesma dimensionalidade.  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir retorna os anos de 2003 e 2004, os dois membros que aparecem em ambos os conjuntos especificados:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 A consulta a seguir falha porque os dois conjuntos especificados contêm membros de hierarquias diferentes:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
