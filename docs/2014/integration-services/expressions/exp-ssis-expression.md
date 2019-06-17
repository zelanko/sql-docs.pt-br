---
title: EXP (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 366a938b2e90ce448cbcba2775f0eb7f327aab61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62898051"
---
# <a name="exp-ssis-expression"></a>EXP (Expressão SSIS)
  Retorna o expoente para a base e de uma expressão numérica. A função EXP complementa a ação da função LN e, às vezes, é chamado de antilogaritmo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Comentários  
 A expressão numérica é lançada para o tipo de dados de DT_R8 antes de o expoente ser computado. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 O resultado de retorno sempre é um número positivo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Estes exemplos se aplicam à função EXP para valores positivo e negativos e para zero.  
  
```  
EXP(74)  
```  
  
 Retorna 1.373382979540176E+32.  
  
```  
EXP(-27)  
```  
  
 Retorna 1.879528816539083E-12.  
  
```  
EXP(0)  
```  
  
 Retorna 1.  
  
## <a name="see-also"></a>Consulte também  
 [LOG &#40;Expressão SSIS&#41;](log-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
