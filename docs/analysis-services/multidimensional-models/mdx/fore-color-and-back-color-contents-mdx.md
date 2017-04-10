---
title: "Conte&#250;do de FORE_COLOR e BACK_COLOR (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conteúdo de FORE_COLOR"
  - "planos de fundo [MDX]"
  - "células [MDX]"
  - "cores [MDX]"
  - "armazenando informações de cor da célula"
  - "planos de fundo de célula"
  - "conteúdo de BACK_COLOR"
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Conte&#250;do de FORE_COLOR e BACK_COLOR (MDX)
  As propriedades de célula **FORE_COLOR** e **BACK_COLOR** armazenam informações sobre a cor do texto e da tela de fundo de uma célula, respectivamente, no formato RGB (vermelho, verde e azul) do sistema operacional Microsoft Windows.  
  
 O intervalo válido para uma cor RGB comum vai de zero (0) a 16.777.215 (&H00FFFFFF). O byte mais elevado de um número desse intervalo é sempre igual a 0; os 3 bytes mais baixos, do menos importante para o mais importante, determinam o valor de vermelho, verde e azul, respectivamente. Cada um dos componentes vermelho, verde e azul é representado por um número entre 0 e 255 (&HFF).  
  
## Consulte também  
 [Usando propriedades da célula &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-cell-properties-mdx.md)  
  
  