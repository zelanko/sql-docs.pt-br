---
title: Instrução CALCULATE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 389c5f470cb3bf00cfe668a9405e36cd4ac8950e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187631"
---
# <a name="mdx-scripting---calculate"></a>Script MDX – CALCULATE


  Popula cada célula em um cubo com um valor de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argumentos  
 None  
  
## <a name="remarks"></a>Comentários  
 A instrução CALCULATE é incluída automaticamente como a primeira instrução no script MDX de um cubo ao criar um cubo usando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A instrução CALCULATE informa cada célula no cubo a ser agregada a partir das células de granularidade inferior. Após uma célula ser agregada, se as células de granularidade inferior forem populadas consecutivamente com expressões, o valor agregado das células de granularidade superior será afetado. Você quase sempre deseja realizar essa agregação, mas é possível removê-la ou fazer com que outras instruções executem essa instrução antes.  
  
 A instrução CALCULATE não pode ser incluída em um subcubo aninhado no script MDX. Um subcubo aninhado é definido com a instrução SCOPE. Para obter mais informações sobre a instrução SCOPE, consulte [instrução SCOPE &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Os membros calculados não são agregados.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [Conceitos básicos do script MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Definir atribuições e outros comandos de script](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  
