---
title: (Divisão) (DMX) | Microsoft Docs
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
- / (divide)
- divide operator (/)
ms.assetid: 7afc06cd-054b-48c3-9c3c-9a0c17d15e63
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 00e4712dd44860c673f67d62d7eb1d6ff0bd5d5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="divide-dmx"></a>(Divisão) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação aritmética que divide um número por outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *dividendo*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
 *divisor*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Valor que possui o tipo de dados do parâmetro que tem prioridade alta.  
  
## <a name="remarks"></a>Remarks  
 O valor que esse operador retorna representa o quociente da primeira expressão dividido pela segunda expressão.  
  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se o divisor avaliar um valor nulo, o operador apresentará um erro. Se ambos, o divisor e o dividendo avaliarem um valor nulo, o operador retornará um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Operadores aritméticos &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Dividir &#40;expressão SSIS&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;Dividir&#41; &#40;Transact-SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
