---
title: "- (Subtra&#231;&#227;o) (Express&#227;o SSIS) | Microsoft Docs"
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
  - "- (subtrair)"
  - "operador de subtração (-)"
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# - (Subtra&#231;&#227;o) (Express&#227;o SSIS)
  Subtrai a segunda expressão numérica da primeira.  
  
## Sintaxe  
  
```  
  
numeric_expression1 – numeric_expression2  
  
```  
  
## Argumentos  
 *numeric_expression1, numeric_expression2*  
 É qualquer expressão válida de um tipo de dados numérico. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Tipos de resultado  
 Determinado pelos tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Comentários  
 Coloque a expressão unária minus em parênteses para assegurar que ela seja avaliada na ordem correta  
  
## Comentários  
 Se qualquer operando for nulo, o resultado será nulo.  
  
## Exemplos de expressões  
 Este exemplo subtrai literais numéricas.  
  
```  
5 - 6.09  
```  
  
 Este exemplo subtrai o valor na coluna **StandardCost** do valor na coluna **ListPrice**.  
  
```  
ListPrice - StandardCost  
```  
  
 Este exemplo subtrai um valor calculado da coluna **ListPrice**. A variável **Discount%** deve estar entre colchetes porque o nome inclui o caractere % . Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## Consulte também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  