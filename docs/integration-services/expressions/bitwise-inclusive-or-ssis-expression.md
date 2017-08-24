---
title: "| (Bit a bit OR inclusivo) (Expressão SSIS) | Microsoft Docs"
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
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 90a8167d52a50c569418af86d4f36526ad3482c0
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>| (OR inclusivo de bit a bit) (Expressão SSIS)
  Executa uma operação OR de bit a bit de dois valores de inteiro. Compara cada bit de seu primeiro operando com o bit correspondente de seu segundo operando. Se qualquer bit for 1, o bit de resultado correspondente será definido como 1. Caso contrário, o bit de resultado correspondente é definido como zero (0).  
  
 Ambas as condições devem ser um tipo de dados inteiro assinado ou ambas as condições devem ser um tipo de dados inteiro não assinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression1, integer_ expression2*  
 É qualquer expressão válida de um tipo de dados inteiro assinado ou não assinado. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentários  
 Se qualquer condição for nula, o resultado de expressão será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo executa uma operação OR de bit a bit inclusiva entre as variáveis **NumberA** e **NumberB**. **NumberA** contém 3 (00000011) e **NumberB** contém 9 (00001001).  
  
```  
@NumberA | @NumberB  
```  
  
 A expressão é avaliada como 11 (00001011).  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 Este exemplo executa uma operação OR de bit a bit inclusiva entre as colunas **ReorderPoint** e **SafetyStockLevel** .  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 Se **ReorderPoint** for 10 e **SafetyStockLevel** for 8, a expressão será avaliada como 10 (00001010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 Este exemplo executa uma operação OR de bit a bit inclusiva entre dois inteiros.  
  
```  
3 | 5   
```  
  
 A expressão é avaliada como 7 (00000111).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## <a name="see-also"></a>Consulte também  
 [&#124; &#124; &#40; OR lógico &#41; &#40; Expressão do SSIS &#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^ &#40; Bit a bit exclusivo ou &#41; &#40; Expressão do SSIS &#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Precedência do operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40; Expressão SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
