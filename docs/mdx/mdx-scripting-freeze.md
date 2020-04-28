---
title: CONGELAR instrução (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4738dab411fe55808034a6d9d81a16994089ea74
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68138286"
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
  
  
