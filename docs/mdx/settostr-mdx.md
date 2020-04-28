---
title: SetToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3965c3cc8ea2a2f2de292ca0c75e49c957e04f02
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036974"
---
# <a name="settostr-mdx"></a>SetToStr (MDX)


  Retorna uma cadeia com formato da linguagem MDX que corresponde a um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 Essa função é usada para transferir uma representação de cadeia de caracteres de um conjunto para análise de uma função externa. A cadeia de caracteres retornada é colocada entre chaves {}, com cada item no conjunto separado por uma vírgula.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna uma cadeia de caracteres que contém todos os membros da hierarquia de atributo Geography.Country.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
