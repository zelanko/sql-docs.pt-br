---
title: "^ (OR exclusivo de bit a bit) (Express&#227;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "^ (operador OR exclusivo de bit a bit)"
  - "OR exclusivo de bit a bit (^)"
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# ^ (OR exclusivo de bit a bit) (Express&#227;o SSIS)
  Executa uma operação OR de bit a bit exclusiva de dois valores inteiros. Compara cada bit de seu primeiro operando com o bit correspondente de seu segundo operando. Se um bit for 0 e o outro bit for 1, o bit de resultado correspondente será definido como 1. Se ambos os bits forem 0 ou ambos os bits forem 1, o bit de resultado correspondente será definido como 0.  
  
 Ambas as condições devem ser um tipo de dados inteiro assinado ou ambas as condições devem ser um tipo de dados inteiro não assinado.  
  
## Sintaxe  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## Argumentos  
 *integer_expression1, integer_expression2*  
 É qualquer expressão válida de um tipo de dados inteiro assinado ou não assinado. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Comentários  
 Se qualquer condição for nula, o resultado de expressão será nulo.  
  
## Exemplos de expressões  
 Este exemplo executa uma operação OR de bit a bit exclusiva entre as variáveis **NumberA** e **NumberB**. **NumberA** contém 3 (00000011) e **NumberB** contém 7 (00000111).  
  
```  
@NumberA ^ @NumberB  
```  
  
 A expressão é avaliada como 4 (00000100).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 Este exemplo executa uma operação OR de bit a bit exclusiva entre as colunas **ReorderPoint** e **SafetyStockLevel** .  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 Se **ReorderPoint** for 10 e **SafetyStockLevel** for 8, a expressão será avaliada como 2 (00000010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 Este exemplo executa uma operação OR de bit a bit exclusiva entre dois inteiros.  
  
```  
3 ^ 5   
```  
  
 A expressão é avaliada como 6 (00000110).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## Consulte também  
 [&#124;&#124; &#40;OR lógica&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [&#124; &#40;OR inclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  