---
title: "&amp;&amp; (AND l&#243;gico) (Express&#227;o SSIS) | Microsoft Docs"
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
  - "&& (AND lógico)"
  - "AND, AND lógico"
  - "AND lógico (&&)"
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# &amp;&amp; (AND l&#243;gico) (Express&#227;o SSIS)
  Executa uma operação AND lógica. A expressão será avaliada como TRUE se todas as condições forem TRUE.  
  
## Sintaxe  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## Argumentos  
 *boolean _expression1, boolean_expression2*  
 É qualquer expressão válida que é avaliada como TRUE, FALSE ou NULL.  
  
## Tipos de resultado  
 DT_BOOL  
  
## Comentários  
 A tabela a seguir mostra o resultado do operador &&.  
  
|Resultado|Expressão|Expressão|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## Exemplos de expressões  
 Este exemplo usa **StandardCost** e as colunas **ListPrice**. O exemplo avaliará como TRUE se o valor da coluna **StandardCost** for menor que 300 e a coluna **ListPrice** for maior que 500.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 Este exemplo usa as variáveis **SPrice** e **LPrice** em vez de literais.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## Consulte também  
 [& &#40;AND bit a bit&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  