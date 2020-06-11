---
title: = (Igual a) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0633540153f2dd9dfd60831a58744ea2d6331fbd
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670293"
---
# <a name="-equal-to-dmx"></a>= (Igual a) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão DMX (Data Mining Extensions) é igual ao valor de outra expressão DMX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DMX_Expression = DMX_Expression   
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DMX_Expression*  
 Expressão DMX válida.  
  
## <a name="return-value"></a>Valor Retornado  
 Valor Booliano que conterá TRUE se ambos os parâmetros forem não nulos e se o valor do primeiro parâmetro for igual ao valor do segundo parâmetro. O valor Booliano conterá FALSE se ambos os parâmetros forem não nulos e o valor do primeiro parâmetro for diferente do valor do segundo parâmetro. O valor Booliano conterá um valor nulo se um ou ambos os parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores de comparação &#40;&#41;DMX](../dmx/operators-comparison.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)  
  
  
