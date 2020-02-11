---
title: Dividir (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6184aa9d932355cd935a9131848ec27895faea5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049302"
---
# <a name="divide-mdx"></a>Dividir (MDX)


  Efetua a divisão e retorna um resultado alternativo ou BLANK() na divisão por zero.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *numerator*  
 O dividendo ou o número a ser dividido.  
  
 *denominator*  
 O divisor ou o número para dividir.  
  
 *alternateresult*  
 (Opcional) O valor retornado quando a divisão por zero resulta em um erro. Quando não fornecido, o valor padrão é BLANK().  
  
## <a name="remarks"></a>Comentários  
 O resultado alternativo na divisão por zero deve ser uma constante.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
