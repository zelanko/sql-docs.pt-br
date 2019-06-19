---
title: + (Concatenação de cadeia de caracteres) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 292d671fb3b971c30b6e261e3b851aba1ead9b36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150012"
---
# <a name="-string-concatenation-mdx"></a>+ (Concatenação de cadeia de caracteres) (MDX)


  Executa uma operação de cadeia de caracteres que concatena duas ou mais cadeias de caracteres, tuplas ou uma combinação de cadeias de caracteres e tuplas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *String_Expression*  
 Uma linguagem MDX válida que retorna um valor de cadeia de caracteres.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor com o tipo de dados do parâmetro com prioridade maior.  
  
## <a name="remarks"></a>Comentários  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão avaliar a um valor nulo, o operador retornará o resultado da outra expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
