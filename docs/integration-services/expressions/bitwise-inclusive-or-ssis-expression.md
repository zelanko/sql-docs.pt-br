---
title: '| (OR inclusivo bit a bit) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 17a92a32fba02d8c4da167d412d02eed0d5f6b77
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71290409"
---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>| (OR inclusivo de bit a bit) (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="see-also"></a>Consulte Também  
 [&#124;&#124; &#40;OR lógica&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^ &#40;OR exclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
