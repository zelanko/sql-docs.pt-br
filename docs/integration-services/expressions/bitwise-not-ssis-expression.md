---
title: "~ (Not bit a bit) (expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 398f902d224f49e00b3fdc62bf39300ba180fda8
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="-bitwise-not-ssis-expression"></a>~ (Não de bit a bit) (Expressão SSIS)
  Executa uma negação bit a bit de um inteiro. Esse operador pode ser se aplicado a tipos de dados inteiro assinados e não assinados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression*  
 É qualquer expressão válida de um tipo de dados inteiro. *integer*_*expression* é um inteiro que é transformado em um número binário para a operação bit a bit. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados de *integer_expression.*  
  
## <a name="remarks"></a>Comentários  
 Nenhum.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esse exemplo executa uma operação ~ (NOT) bit a bit no número 170 (0000 0000 1010 1010). O número é um inteiro assinado.  
  
```  
  
~ 170  
```  
  
 A expressão é avaliada como -170 (1111111101010101).  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>Consulte também  
 [Precedência do operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40; Expressão SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

