---
title: Usando funções lógicas | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- logical functions [MDX]
ms.assetid: 0cb34d53-9146-4924-9c9b-607afcb7a2be
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5aa920ccc64ad0d5236574283529fbf934c3db92
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-logical-functions"></a>Usando funções lógicas
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Uma função lógica executa uma operação ou comparação lógica em objetos e expressões e retorna um valor booliano. As funções lógicas são essenciais na linguagem MDX para determinar a posição de um membro.  
  
 A função lógica mais comumente usada é a **IsEmpty** função. Para obter mais informações sobre como usar o **IsEmpty** funcionam, consulte [trabalhando com valores vazios](../mdx/working-with-empty-values.md).  
  
 A consulta a seguir mostra como usar o **IsLeaf** e **IsAncestor** funções:  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;sintaxe MDX&#41;](../mdx/functions-mdx-syntax.md)  
  
  
