---
title: Divide (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86b4d8c97996733396e3062e134b2e31d2819ec0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471307"
---
# <a name="divide-mdx"></a>Dividir (MDX)


  Efetua a divisão e retorna um resultado alternativo ou BLANK() na divisão por zero.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *numerator*  
 O dividendo ou número para dividir.  
  
 *denominator*  
 O divisor ou número pelo qual dividir.  
  
 *alternateresult*  
 (Opcional) O valor retornado quando a divisão por zero resulta em um erro. Quando não fornecido, o valor padrão é BLANK().  
  
## <a name="remarks"></a>Comentários  
 O resultado alternativo na divisão por zero deve ser uma constante.  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
