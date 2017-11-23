---
title: "- (Subtração) (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: 9602e908-e80c-442a-a412-073e10d0abd4
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d1156dfc98cc1d2fd5d91e9f54fd0ab4001fa2b0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="--subtract-dmx"></a>- (Subtrair) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação aritmética que subtrai um número do outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric_Expression - Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Numeric_Expression*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Valor que possui o tipo de dados do parâmetro que tem prioridade alta.  
  
## <a name="remarks"></a>Comentários  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão avaliar a um valor nulo, o operador retornará o resultado da outra expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Aritmética operadores &#40; DMX &#41;](../dmx/operators-arithmetic.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
