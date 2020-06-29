---
title: '&amp;&amp; (AND lógico) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2dd2456bfada856e9f9e78e95a7d7561a2413dc2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428353"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (AND lógico) (Expressão SSIS)
  Executa uma operação AND lógica. A expressão será avaliada como TRUE se todas as condições forem TRUE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean _expression1, boolean_expression2*  
 É qualquer expressão válida que é avaliada como TRUE, FALSE ou NULL.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir mostra o resultado do operador &&.  
  
|Result|Expression|Expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULO|NULO|NULO|  
|NULO|NULO|TRUE|  
|FALSE|NULO|FALSE|  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo usa **StandardCost** e as colunas **ListPrice** . O exemplo avaliará como TRUE se o valor da coluna **StandardCost** for menor que 300 e a coluna **ListPrice** for maior que 500.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 Este exemplo usa as variáveis **SPrice** e **LPrice** em vez de literais.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Consulte Também  
 [& &#40;AND bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-and-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
