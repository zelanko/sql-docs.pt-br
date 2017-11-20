---
title: "POWER (expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- POWER function
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d0f4c9e1509dd69af6bc12c6d00c17585fe23552
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="power-ssis-expression"></a>POWER (Expressão SSIS)
  Retorna o resultado da elevação de uma expressão numérica a uma potência. O parâmetro de potência deve ser avaliado como um inteiro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida.  
  
 *power*  
 É uma expressão numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Comentários  
 Os argumentos *numeric_expression* e *power* são convertidos para o tipo de dados de DT_R8 antes de a potência ser calculada. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Se *numeric_expression* for avaliado como zero e *power* for negativo, o avaliador de expressão retornará um erro e definirá o resultado de retorno como nulo.  
  
 Se *numeric_expression* ou *power* forem avaliados como resultados indeterminados, o resultado de retorno será nulo.  
  
 O argumento *power* pode ser uma fração. Por exemplo, você pode usar o valor 0.5 como a potência.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esse exemplo usa um literal numérico. A função eleva 4 à potência de 3 e retorna 64.  
  
```  
POWER(4,3)  
```  
  
 Este exemplo usa a coluna **Length** e a variável **DimensionCount** . Se **Length** for 8, e **DimensionCount** for 2, o resultado de retorno será 64.  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40; Expressão do SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

