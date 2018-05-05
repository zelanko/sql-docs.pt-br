---
title: + (Adicionar) (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- + (add)
- add operator (+)
ms.assetid: 35e7636f-814c-44c3-94a7-384a305d65ea
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b28cf10467c7c321c60ba0a433fc1c883d58d403
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="-add-dmx"></a>+ (Adicionar) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação aritmética que adiciona simultaneamente dois números.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric_Expression + Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Numeric_Expression*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Valor que possui o tipo de dados do parâmetro que tem prioridade alta.  
  
## <a name="remarks"></a>Remarks  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão avaliar a um valor nulo, o operador retornará o resultado da outra expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Operadores aritméticos &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
