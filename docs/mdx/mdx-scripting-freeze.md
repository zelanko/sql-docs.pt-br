---
title: Instrução FREEZE (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b7eb3a3939ce8525dc57d27a24ac005ecb2cf2d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579898"
---
# <a name="mdx-scripting---freeze"></a>Script MDX - CONGELAR
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Bloqueia os valores de célula de um subcubo especificado para seus valores atuais. Quando os valores de célula são bloqueados, as alterações nas outras células não têm nenhum efeito nas células que estão bloqueadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>Argumentos  
 *Subcube_Expression*  
 Uma linguagem MDX válida que retorna um subcubo.  
  
## <a name="remarks"></a>Remarks  
 O **CONGELAR** instrução bloqueia os valores de células em um subcubo especificado, impedindo que instruções subsequentes no MDX script alterem seus valores em cálculo subsequente passa.  
  
 No exemplo a seguir, A e B representam subcubos em um script de cálculo MDX:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 Nesse momento, A e B são iguais a 3.  
  
 Agora podemos inserir a **congelar** função para bloquear as células no subcubo:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 Agora, A é igual a 2 e B é igual a 3.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
