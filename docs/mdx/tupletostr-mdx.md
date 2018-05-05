---
title: TupleToStr (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TUPLETOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- TupletoStr function
ms.assetid: ad12347c-d1c4-4d8b-a910-3116bd6b68e0
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6a49e2ffcaca8ae68b2c88f0877bab867746f1da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna uma cadeia com formato da linguagem MDX que corresponde a uma tupla especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
## <a name="remarks"></a>Remarks  
 Essa função é usada para transferir uma representação de cadeia de caracteres de uma tupla para análise de uma função externa. A cadeia de caracteres retornada está entre chaves {} e cada membro, se mais de um for expressamente definido na tupla, é separado por uma vírgula.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte retorna a cadeia de caracteres ([Date].[Calendar Year].&[2001],[Geography].[Geography].[Country].&[United States]):  
  
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
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
