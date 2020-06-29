---
title: SIGN (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2822c1390b7807c60eecfad1d4ba41eaa232b16a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437113"
---
# <a name="sign-ssis-expression"></a>SIGN (Expressão SSIS)
  Retorna o sinal positivo (+1), negativo (-1) ou zero (0) de uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica assinada válida. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 SIGN retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o sinal de um literal numérico. O resultado de retorno é -1.  
  
```  
SIGN(-123.45)  
```  
  
 Este exemplo retorna o sinal do resultado da subtração da coluna **StandardCost** da coluna **DealerPrice** .  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
