---
title: Instrução CALCULATE (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 603d36e9c099ab6148e2e7c485f9c40ad99f63a8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579938"
---
# <a name="mdx-scripting---calculate"></a>Script MDX - CALCULAR
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Popula cada célula em um cubo com um valor de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhum  
  
## <a name="remarks"></a>Remarks  
 A instrução CALCULATE é incluída automaticamente como a primeira instrução no script MDX de um cubo ao criar um cubo usando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A instrução CALCULATE informa cada célula no cubo a ser agregada a partir das células de granularidade inferior. Após uma célula ser agregada, se as células de granularidade inferior forem populadas consecutivamente com expressões, o valor agregado das células de granularidade superior será afetado. Você quase sempre deseja realizar essa agregação, mas é possível removê-la ou fazer com que outras instruções executem essa instrução antes.  
  
 A instrução CALCULATE não pode ser incluída em um subcubo aninhado no script MDX. Um subcubo aninhado é definido com a instrução SCOPE. Para obter mais informações sobre a instrução SCOPE, consulte [instrução SCOPE &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Os membros calculados não são agregados.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [Conceitos básicos de script MDX &#40;do Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Definir atribuições e outros comandos de script](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  
