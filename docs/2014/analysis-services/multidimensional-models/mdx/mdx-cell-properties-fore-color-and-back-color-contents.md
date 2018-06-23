---
title: Conteúdo de FORE_COLOR e BACK_COLOR conteúdo (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
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
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e7e22839611c1a9060b66850371d0ac2b551337c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011248"
---
# <a name="forecolor-and-backcolor-contents-mdx"></a>Conteúdo de FORE_COLOR e BACK_COLOR (MDX)
  As propriedades de célula `FORE_COLOR` e `BACK_COLOR` armazenam informações sobre a cor do texto e do plano de fundo de uma célula, respectivamente, no formato RGB (vermelho, verde e azul) do sistema operacional Microsoft Windows.  
  
 O intervalo válido para uma cor RGB comum vai de zero (0) a 16.777.215 (&H00FFFFFF). O byte mais elevado de um número desse intervalo é sempre igual a 0; os 3 bytes mais baixos, do menos importante para o mais importante, determinam o valor de vermelho, verde e azul, respectivamente. Cada um dos componentes vermelho, verde e azul é representado por um número entre 0 e 255 (&HFF).  
  
## <a name="see-also"></a>Consulte também  
 [Usando propriedades de célula &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  