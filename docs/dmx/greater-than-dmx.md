---
title: '&gt;(Maior que) (DMX) | Microsoft Docs'
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: a1485c02-8d10-4722-b8cd-b747c472741b
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 58c959cb74a2a6b402cdfba2b80a1dca82d56a0f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="gt-greater-than-dmx"></a>&gt;(Maior que) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão DMX (Data Mining Extensions) é maior do que o valor de outra expressão DMX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DMX_Expression > DMX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DMX_Expression*  
 Expressão DMX válida.  
  
## <a name="return-value"></a>Valor de retorno  
 Valor booliano que conterá TRUE se ambos os parâmetros forem não nulos e se o primeiro parâmetro tiver um valor maior do que o valor do segundo parâmetro. O valor booliano conterá FALSE se ambos os parâmetros forem não nulos e se o primeiro parâmetro tiver um valor igual a ou menor do que o valor do segundo parâmetro. O valor Booliano conterá um valor nulo se um ou ambos os parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores de comparação &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
