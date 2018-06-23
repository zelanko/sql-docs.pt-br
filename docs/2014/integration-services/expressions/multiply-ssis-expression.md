---
title: '* (Multiplicar) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a65d028ec5c9fd739c59b3d4bf5f89c622b4d5f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116410"
---
# <a name="-multiply-ssis-expression"></a>* (Multiplicar) (Expressão SSIS)
  Multiplica duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression1, numeric_expression2*  
 É qualquer expressão válida de um tipo de dados numérico. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Se qualquer operando for nulo, o resultado será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo multiplica literais numéricos.  
  
```  
5 * 6.09  
```  
  
 Este exemplo multiplica valores na coluna **ListPrice** por 10%.  
  
```  
ListPrice * .10  
```  
  
 Este exemplo subtrai o resultado de uma expressão da coluna **ListPrice** . A variável **Discount%** deve estar entre colchetes porque o nome inclui o caractere % . Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Precedência do operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;expressão SSIS&#41;](operators-ssis-expression.md)  
  
  