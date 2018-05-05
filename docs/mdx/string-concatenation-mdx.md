---
title: + (Concatenação de cadeia de caracteres) (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- +
dev_langs:
- kbMDX
helpviewer_keywords:
- string concatenation operators
- + (string concatenation)
ms.assetid: d77636b1-2973-4587-af35-54aba5700d9a
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6ce74b5fb7e3123db674e318cf8340fed974c591
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="-string-concatenation-mdx"></a>+ (Concatenação de cadeia de caracteres) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão avaliar a um valor nulo, o operador retornará o resultado da outra expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
