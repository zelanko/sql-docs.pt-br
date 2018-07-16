---
title: '&amp;&amp; (AND lógico) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0185c28d970a1698a4159daefbbca9338b2a66cb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302256"
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
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir mostra o resultado do operador &&.  
  
|Resultado|Expression|Expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo usa **StandardCost** e as colunas **ListPrice** . O exemplo avaliará como TRUE se o valor da coluna **StandardCost** for menor que 300 e a coluna **ListPrice** for maior que 500.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 Este exemplo usa as variáveis **SPrice** e **LPrice** em vez de literais.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Consulte também  
 [& &#40;AND bit a bit&#41; &#40;expressão do SSIS&#41;](bitwise-and-ssis-expression.md)   
 [Associatividade e precedência de operador](operator-precedence-and-associativity.md)   
 [Operadores &#40;expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
