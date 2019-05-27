---
title: Conteúdo FORE_COLOR e Back_color (MDX) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ecd8bb157d7b501d29230c91d87f148ae738ff45
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074407"
---
# <a name="forecolor-and-backcolor-contents-mdx"></a>Conteúdo de FORE_COLOR e BACK_COLOR (MDX)
  As propriedades de célula `FORE_COLOR` e `BACK_COLOR` armazenam informações sobre a cor do texto e do plano de fundo de uma célula, respectivamente, no formato RGB (vermelho, verde e azul) do sistema operacional Microsoft Windows.  
  
 O intervalo válido para uma cor RGB comum vai de zero (0) a 16.777.215 (&H00FFFFFF). O byte mais elevado de um número desse intervalo é sempre igual a 0; os 3 bytes mais baixos, do menos importante para o mais importante, determinam o valor de vermelho, verde e azul, respectivamente. Cada um dos componentes vermelho, verde e azul é representado por um número entre 0 e 255 (&HFF).  
  
## <a name="see-also"></a>Consulte também  
 [Usando propriedades da célula &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  
