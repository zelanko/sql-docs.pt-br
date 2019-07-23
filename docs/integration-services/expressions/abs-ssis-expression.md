---
title: ABS (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 00f3937c13de5db106732ee919db6671485b691f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057667"
---
# <a name="abs-ssis-expression"></a>ABS (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>Remarks  
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
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
