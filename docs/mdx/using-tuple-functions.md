---
description: Usando funções de tupla
title: Usando funções de tupla | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d858fa6e67712a6ab93608dae20a15dca629c01e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500489"
---
# <a name="using-tuple-functions"></a>Usando funções de tupla


  Uma função de tupla recupera uma tupla de um conjunto ou recupera uma, resolvendo a representação de cadeia de caracteres de uma tupla.  
  
 As funções de tupla, assim como as funções de membro e de conjunto, são essenciais para negociar as estruturas multidimensionais encontradas no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Há três funções de tupla em MDX, [atual &#40;mdx&#41;](../mdx/current-mdx.md), [Item &#40;tupla&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md) e [StrToTuple &#40;MDX ](../mdx/strtotuple-mdx.md)&#41;. A consulta de exemplo a seguir mostra como usar cada uma:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of Years and Countries`  
  
 `SET MyTuples AS  [Date].[Calendar Year].[Calendar Year].MEMBERS * [Customer].[Country].[Country].MEMBERS`  
  
 `//Returns a string representation of that set using the Current and Generate functions`  
  
 `MEMBER MEASURES.CURRENTDEMO AS GENERATE(MyTuples, TUPLETOSTR(MyTuples.CURRENT), ", ")`  
  
 `//Retrieves the fourth tuple from that set and displays it as a string`  
  
 `MEMBER MEASURES.ITEMDEMO AS TUPLETOSTR(MyTuples.ITEM(3))`  
  
 `//Creates a tuple consisting of the measure Internet Sales Amount and the country Australia from a string`  
  
 `MEMBER MEASURES.STRTOTUPLEDEMO AS STRTOTUPLE("([Measures].[Internet Sales Amount]" + ", [Customer].[Country].&[Australia])")`  
  
 `SELECT{MEASURES.CURRENTDEMO,MEASURES.ITEMDEMO,MEASURES.STRTOTUPLEDEMO} ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;sintaxe MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Usando funções de membro](../mdx/using-member-functions.md)   
 [Usando funções de conjunto](../mdx/using-set-functions.md)  
  
  
