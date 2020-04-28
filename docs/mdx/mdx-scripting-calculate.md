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
ms.openlocfilehash: a873c2a6a60e3e6283c3c24fa4b9d28757e57ffb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893351"
---
# <a name="mdx-scripting---calculate"></a>Script MDX – CALCULATE


  Popula cada célula em um cubo com um valor de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 A instrução CALCULATE é incluída automaticamente como a primeira instrução no script MDX de um cubo ao criar um cubo usando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A instrução CALCULATE informa cada célula no cubo a ser agregada a partir das células de granularidade inferior. Após uma célula ser agregada, se as células de granularidade inferior forem populadas consecutivamente com expressões, o valor agregado das células de granularidade superior será afetado. Você quase sempre deseja realizar essa agregação, mas é possível removê-la ou fazer com que outras instruções executem essa instrução antes.  
  
 A instrução CALCULATE não pode ser incluída em um subcubo aninhado no script MDX. Um subcubo aninhado é definido com a instrução SCOPE. Para obter mais informações sobre a instrução SCOPE, consulte [instrução scope &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Os membros calculados não são agregados.  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de script MDX &#40;&#41;MDX](../mdx/mdx-scripting-statements-mdx.md)   
 [Conceitos básicos de script MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [Definir atribuições e outros comandos de script](https://docs.microsoft.com/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
  
