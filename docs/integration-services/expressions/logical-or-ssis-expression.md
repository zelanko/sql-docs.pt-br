---
description: '|| (OR lógico) (Expressão SSIS)'
title: '|| (OR lógico) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b613adbf102e1103506e6d86efb3bf87d81d72eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88347542"
---
# <a name="-logical-or-ssis-expression"></a>|| (OR lógico) (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Executa uma operação OR lógica. A expressão será avaliada como TRUE se uma ou ambas as condições forem TRUE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression1, boolean_expression2*  
 É qualquer expressão válida que é avaliada como TRUE, FALSE ou NULL.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir mostra o resultado do operador ||.  
  
|Result|Expression|Expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULO|NULO|NULO|  
|TRUE|NULO|TRUE|  
|NULO|NULO|FALSE|  
  
## <a name="ssis-expression-examples"></a>Exemplos de expressões SSIS  
 Este exemplo usa as colunas **StandardCost** e **ListPrice** . O exemplo será avaliado como TRUE se o valor da coluna **StandardCost** for menor que 300 ou a coluna **ListPrice** for maior que 500.  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 Este exemplo usa as variáveis **SPrice** e **LPrice** em vez de literais numéricos.  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#124; &#40;OR inclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [^ &#40;OR exclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
