---
title: "+ (Adi&#231;&#227;o) (SSIS) | Microsoft Docs"
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
  - "+ (adição)"
  - "operador de adição (+)"
  - "adicionando expressões"
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# + (Adi&#231;&#227;o) (SSIS)
  Soma duas expressões numéricas.  
  
## Sintaxe  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## Argumentos  
 *numeric_expression1, numeric_ expression2*  
 É qualquer expressão válida de um tipo de dados numérico.  
  
## Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Comentários  
 Se qualquer operando for nulo, o resultado será nulo.  
  
## Exemplos de expressões  
 Este exemplo soma literais numéricos.  
  
```  
5 + 6.09 + 7.0  
```  
  
 Este exemplo soma valores nas colunas **VacationHours** e **SickLeaveHours** .  
  
```  
VacationHours + SickLeaveHours  
```  
  
 Este exemplo acrescenta um valor calculado à coluna **StandardCost** . A variável **Profit%** deve estar entre colchetes porque o nome inclui o caractere % . Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## Consulte também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  