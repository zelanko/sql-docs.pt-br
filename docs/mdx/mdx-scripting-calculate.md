---
title: Instrução CALCULATE (MDX) | Microsoft Docs
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
- CALCULATE
dev_langs:
- kbMDX
helpviewer_keywords:
- CALCULATE statement
ms.assetid: 41e196a1-d49e-487b-a42a-73e5d441ed1b
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9be6ad404ade5784ab86845b90cda51b2b939bdf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-scripting---calculate"></a>Script MDX - CALCULAR
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Popula cada célula em um cubo com um valor de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 A instrução CALCULATE é incluída automaticamente como a primeira instrução no script MDX de um cubo ao criar um cubo usando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A instrução CALCULATE informa cada célula no cubo a ser agregada a partir das células de granularidade inferior. Após uma célula ser agregada, se as células de granularidade inferior forem populadas consecutivamente com expressões, o valor agregado das células de granularidade superior será afetado. Você quase sempre deseja realizar essa agregação, mas é possível removê-la ou fazer com que outras instruções executem essa instrução antes.  
  
 A instrução CALCULATE não pode ser incluída em um subcubo aninhado no script MDX. Um subcubo aninhado é definido com a instrução SCOPE. Para obter mais informações sobre a instrução SCOPE, consulte [instrução SCOPE &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Os membros calculados não são agregados.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [Conceitos básicos de script MDX & #40; Analysis Services & #41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Definir atribuições e outros comandos de script](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  
