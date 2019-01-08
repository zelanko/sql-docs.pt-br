---
title: ^ (OR exclusivo bit a bit) (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7d29154f00659680bbd0dd7106d65fe1e058ad7c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793598"
---
# <a name="-bitwise-exclusive-or-ssis-expression"></a>^ (OR exclusivo de bit a bit) (Expressão SSIS)
  Executa uma operação OR de bit a bit exclusiva de dois valores inteiros. Compara cada bit de seu primeiro operando com o bit correspondente de seu segundo operando. Se um bit for 0 e o outro bit for 1, o bit de resultado correspondente será definido como 1. Se ambos os bits forem 0 ou ambos os bits forem 1, o bit de resultado correspondente será definido como 0.  
  
 Ambas as condições devem ser um tipo de dados inteiro assinado ou ambas as condições devem ser um tipo de dados inteiro não assinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression1, integer_expression2*  
 É qualquer expressão válida de um tipo de dados inteiro assinado ou não assinado. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Comentários  
 Se qualquer condição for nula, o resultado de expressão será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
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
  
## <a name="see-also"></a>Consulte também  
 [&#124;&#124; &#40;OR lógica&#41; &#40;Expressão SSIS&#41;](logical-or-ssis-expression.md)   
 [&#124; &#40;OR inclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-inclusive-or-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
