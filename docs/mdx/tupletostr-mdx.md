---
description: TupleToStr (MDX)
title: TupleToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 69e81156b26d4becb05390c8684b433584793697
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487619"
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)


  Retorna uma cadeia de caracteres formatada com MDX (Multidimensional Expressions) que corresponde a uma tupla especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
## <a name="remarks"></a>Comentários  
 Essa função é usada para transferir uma representação de cadeia de caracteres de uma tupla para análise de uma função externa. A cadeia de caracteres retornada é colocada entre chaves {} e cada membro, se mais de um for expressamente definido na tupla, será separado por uma vírgula.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a cadeia de caracteres ([date]. [ Ano civil]. & [2001], [geografia]. [Geografia]. [País]. & [Estados Unidos]):  
  
```  
WITH MEMBER Measures.x AS TupleToStr   
   (   
      ([Date].[Calendar Year].&[2001]  
         , [Geography].[Geography].[Country].&[United States]  
      )  
   )     
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna a mesma cadeia de caracteres como o exemplo anterior.  
  
```  
WITH SET s AS   
   {  
      ([Date].[Calendar Year].&[2001],  
         [Geography].[Geography].[Country].&[United States]  
      )   
   }  
MEMBER Measures.x AS TupleToStr ( s.Item(0) )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
