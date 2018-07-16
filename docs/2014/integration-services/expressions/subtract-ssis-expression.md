---
title: '- (Subtrair) (Expressão SSIS) | Microsoft Docs'
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
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cbceb06967d0bbfb305bd46673c8bbbcb9e1bfcf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324616"
---
# <a name="--subtract-ssis-expression"></a>- (Subtração) (Expressão SSIS)
  Subtrai a segunda expressão numérica da primeira.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
numeric_expression1 – numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression1, numeric_expression2*  
 É qualquer expressão válida de um tipo de dados numérico. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado pelos tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Coloque a expressão unária minus em parênteses para assegurar que ela seja avaliada na ordem correta  
  
## <a name="remarks"></a>Remarks  
 Se qualquer operando for nulo, o resultado será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo subtrai literais numéricas.  
  
```  
5 - 6.09  
```  
  
 Este exemplo subtrai o valor na coluna **StandardCost** do valor na coluna **ListPrice** .  
  
```  
ListPrice - StandardCost  
```  
  
 Este exemplo subtrai um valor calculado da coluna **ListPrice** . A variável **Discount%** deve estar entre colchetes porque o nome inclui o caractere % . Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Associatividade e precedência de operador](operator-precedence-and-associativity.md)   
 [Operadores &#40;expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
