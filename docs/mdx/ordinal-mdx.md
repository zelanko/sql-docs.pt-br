---
title: Ordinal (MDX) | Microsoft Docs
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
- Ordinal
dev_langs:
- kbMDX
helpviewer_keywords:
- Ordinal function
ms.assetid: 9d416c39-da4a-4f0d-8d85-a76af5df0a87
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 05beb0cd39e57df5c67a1d9a536c2e4702a9e4db
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o valor ordinal com base em zero associado a um nível.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
## <a name="remarks"></a>Remarks  
 O **Ordinal** função frequentemente é usada em conjunto com o **IIF** e **CurrentMember** funções para exibir valores diferentes condicionalmente em níveis de hierarquia diferentes, com base na posição ordinal de cada célula específica no resultado da consulta. Por exemplo, você pode usar o **Ordinal** função para executar cálculos em determinados níveis e exibir um valor padrão de "N / a" em outros níveis.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o número ordinal para o nível Trimestre Calendário na hierarquia Calendário.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
