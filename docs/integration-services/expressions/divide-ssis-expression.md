---
title: "(Dividir) (Express&#227;o SSIS) | Microsoft Docs"
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
  - "/ (dividir)"
  - "operador de divisão (/)"
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# (Dividir) (Express&#227;o SSIS)
  Divide a primeira expressão numérica pela segunda.  
  
## Sintaxe  
  
```  
  
dividend / divisor  
  
```  
  
## Argumentos  
 *dividend*  
 É a expressão numérica a ser dividida. *dividend* pode ser qualquer expressão numérica válida. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *divisor*  
 É a expressão numérica pela qual dividir o dividendo. *divisor* pode ser qualquer expressão numérica com exceção de zero.  
  
## Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Comentários  
 Se qualquer operando for nulo, o resultado será nulo.  
  
 Dividir por zero não é legal. Dependendo de como a subexpressão *divisor* é avaliada, um do seguintes erros acontece:  
  
-   Se a subexpressão *divisor* que é avaliada como zero for uma constante, o erro é exibido no tempo de design, fazendo com que a expressão falhe na validação.  
  
-   Se a subexpressão *divisor* avaliada como zero contiver variáveis, mas nenhuma coluna de entrada, o componente ao qual a expressão pertence falhará na validação de pré-execução que ocorre antes de o pacote ser executado.  
  
-   Se a subexpressão *divisor* avaliada como zero contiver as colunas de entrada, o erro será exibido no tempo de execução e será tratado de acordo com as regras do fluxo de erros do componente de fluxo de regras.  
  
## Exemplos de expressões  
 Este exemplo divide dois literais numéricos.  
  
```  
25 / 5  
```  
  
 Este exemplo divide valores na coluna **ListPrice** pelos valores na coluna **StandardCost** .  
  
```  
ListPrice / StandardCost  
```  
  
## Consulte também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  