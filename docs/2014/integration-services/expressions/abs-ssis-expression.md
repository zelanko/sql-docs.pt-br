---
title: ABS (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 79e0c524c2b74b76921f8eafe6f8e4cc47a9f6b5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966696"
---
# <a name="abs-ssis-expression"></a>ABS (Expressão SSIS)
  Retorna o valor positivo absoluto de uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ABS(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica assinada ou não assinada.  
  
## <a name="result-types"></a>Tipos de resultado  
 O tipo de dados da expressão numérica submetido à função.  
  
## <a name="remarks"></a>Comentários  
 ABS retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Estes exemplos se aplicam à função ABS para um número positivo e um negativo. Ambos retornam 1.23.  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 Este exemplo se aplica à função ABS para uma expressão que subtrai valores nas variáveis **HighTemperature** e **LowTempature**.  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
