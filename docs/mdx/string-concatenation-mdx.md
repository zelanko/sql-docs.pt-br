---
description: + (Concatenação de cadeia de caracteres) LINGUAGEM
title: + (Concatenação de cadeia de caracteres) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e92751cb709a93d3d5d8d05ac76361c22bee5fa7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386862"
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
  
## <a name="return-value"></a>Valor de retorno  
 Um valor com o tipo de dados do parâmetro com prioridade maior.  
  
## <a name="remarks"></a>Comentários  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão avaliar a um valor nulo, o operador retornará o resultado da outra expressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
