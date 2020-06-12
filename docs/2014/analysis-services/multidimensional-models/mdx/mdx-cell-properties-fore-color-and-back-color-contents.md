---
title: FORE_COLOR e conteúdo de BACK_COLOR (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 748754ec3c90bb44392d7acb7de8f815be24086e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546411"
---
# <a name="fore_color-and-back_color-contents-mdx"></a>Conteúdo de FORE_COLOR e BACK_COLOR (MDX)
  As propriedades de célula `FORE_COLOR` e `BACK_COLOR` armazenam informações sobre a cor do texto e do plano de fundo de uma célula, respectivamente, no formato RGB (vermelho, verde e azul) do sistema operacional Microsoft Windows.  
  
 O intervalo válido para uma cor RGB comum vai de zero (0) a 16.777.215 (&H00FFFFFF). O byte mais elevado de um número desse intervalo é sempre igual a 0; os 3 bytes mais baixos, do menos importante para o mais importante, determinam o valor de vermelho, verde e azul, respectivamente. Cada um dos componentes vermelho, verde e azul é representado por um número entre 0 e 255 (&HFF).  
  
## <a name="see-also"></a>Consulte Também  
 [Usando propriedades da célula &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  
