---
title: "Usando funções de tupla | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: tuple functions
ms.assetid: fe41e3e5-a675-4169-a966-b42c18e8d741
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4fdb557918f60f19eef47b79796e6f1f49ff1316
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="using-tuple-functions"></a>Usando funções de tupla
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Uma função de tupla recupera uma tupla de um conjunto ou recupera uma, resolvendo a representação de cadeia de caracteres de uma tupla.  
  
 As funções de tupla, assim como as funções de membro e de conjunto, são essenciais para negociar as estruturas multidimensionais encontradas no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Há três funções de tupla em MDX, [atual &#40; MDX &#41; ](../mdx/current-mdx.md), [Item &#40; Coleção de itens &#41; &#40; MDX &#41; ](../mdx/item-tuple-mdx.md) e [StrToTuple &#40; MDX &#41; ](../mdx/strtotuple-mdx.md). A consulta de exemplo a seguir mostra como usar cada uma:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40; Sintaxe MDX &#41;](../mdx/functions-mdx-syntax.md)   
 [Usando funções de membro](../mdx/using-member-functions.md)   
 [Usando funções de conjunto](../mdx/using-set-functions.md)  
  
  
