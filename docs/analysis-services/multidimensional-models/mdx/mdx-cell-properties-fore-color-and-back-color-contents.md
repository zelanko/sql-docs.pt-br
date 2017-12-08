---
title: "Conteúdo de FORE_COLOR e BACK_COLOR conteúdo (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 15eccb9f4951a52bc1cfcf62e15e85eb245eb5f9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-cell-properties---forecolor-and-backcolor-contents"></a>Propriedades de célula MDX - FORE_COLOR e Back_color
  As propriedades de célula **FORE_COLOR** e **BACK_COLOR** armazenam informações sobre a cor do texto e da tela de fundo de uma célula, respectivamente, no formato RGB (vermelho, verde e azul) do sistema operacional Microsoft Windows.  
  
 O intervalo válido para uma cor RGB comum vai de zero (0) a 16.777.215 (&H00FFFFFF). O byte mais elevado de um número desse intervalo é sempre igual a 0; os 3 bytes mais baixos, do menos importante para o mais importante, determinam o valor de vermelho, verde e azul, respectivamente. Cada um dos componentes vermelho, verde e azul é representado por um número entre 0 e 255 (&HFF).  
  
## <a name="see-also"></a>Consulte também  
 [Usando propriedades da célula &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)  
  
  
