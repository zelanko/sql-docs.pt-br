---
title: '|| (OR lógico) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0945d9e749014648b257499374fc9dc41bb511b6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805168"
---
# <a name="-logical-or-ssis-expression"></a>|| (OR lógico) (Expressão SSIS)
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
  
|Resultado|Expression|Expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|TRUE|NULL|TRUE|  
|NULL|NULL|FALSE|  
  
## <a name="ssis-expression-examples"></a>Exemplos de expressões SSIS  
 Este exemplo usa as colunas **StandardCost** e **ListPrice** . O exemplo será avaliado como TRUE se o valor da coluna **StandardCost** for menor que 300 ou a coluna **ListPrice** for maior que 500.  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 Este exemplo usa as variáveis **SPrice** e **LPrice** em vez de literais numéricos.  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Consulte também  
 [&#124; &#40;OR inclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-inclusive-or-ssis-expression.md)   
 [^ &#40;OR exclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-exclusive-or-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
