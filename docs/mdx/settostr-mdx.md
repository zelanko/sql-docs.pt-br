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
manager: kfile
ms.openlocfilehash: 57e74eb1c7db4aebdd01fde8fc48a425d7affa55
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743295"
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
  
## <a name="remarks"></a>Remarks  
 Essa função é usada para transferir uma representação de cadeia de caracteres de um conjunto para análise de uma função externa. A cadeia de caracteres retornada está entre chaves {}, com cada item no conjunto de separados por uma vírgula.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna uma cadeia de caracteres que contém todos os membros da hierarquia de atributo Geography.Country.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
