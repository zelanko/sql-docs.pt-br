---
title: Tupletostr=1=«tupla»=retorna (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f07e71e5b8314320f76be4496744da5a9d9e81a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208458"
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)


  Retorna uma cadeia de caracteres formatada para MDX que corresponde a uma tupla especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
## <a name="remarks"></a>Comentários  
 Essa função é usada para transferir uma representação de cadeia de caracteres de uma tupla para análise de uma função externa. A cadeia de caracteres retornada é colocada entre chaves {} e cada membro, se mais de um for expressamente definido na tupla, é separado por uma vírgula.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a cadeia de caracteres ([Date]. [ Ano civil]. & [2001], [Geography]. [Geography]. [Country]. & [United States]):  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
