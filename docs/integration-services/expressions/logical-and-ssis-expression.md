---
description: '&amp;&amp; (AND lógico) (Expressão SSIS)'
title: '&amp;&amp; (AND lógico) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
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
ms.openlocfilehash: abb14eae98abaad9ebaaf70331abd42300ee4eee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425398"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (AND lógico) (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
 [& &#40;AND bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
