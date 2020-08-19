---
description: Instrução FREEZE (MDX)
title: CONGELAR instrução (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41c71987fec932b2693740792a8d86e200fcf526
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429738"
---
# <a name="mdx-scripting---freeze"></a>Script MDX – FREEZE


  Bloqueia os valores de célula de um subcubo especificado para seus valores atuais. Quando os valores de célula são bloqueados, as alterações nas outras células não têm nenhum efeito nas células que estão bloqueadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>Argumentos  
 *Subcube_Expression*  
 Uma linguagem MDX válida que retorna um subcubo.  
  
## <a name="remarks"></a>Comentários  
 A instrução **Freeze** bloqueia os valores das células em um subcubo especificado, impedindo que instruções subsequentes em um script MDX alterem seus valores em passagens de cálculo subsequentes.  
  
 No exemplo a seguir, A e B representam subcubos em um script de cálculo MDX:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 Nesse momento, A e B são iguais a 3.  
  
 Agora, inserimos a função **Freeze** para bloquear as células no subcubo:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 Agora, A é igual a 2 e B é igual a 3.  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
