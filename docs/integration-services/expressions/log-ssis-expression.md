---
title: "LOG (Express&#227;o SSIS) | Microsoft Docs"
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
  - "logaritmos de base 10"
  - "função LOG"
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# LOG (Express&#227;o SSIS)
  Retorna o logaritmo de base 10 de uma expressão numérica.  
  
## Sintaxe  
  
```  
  
LOG(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida não zero ou não negativa.  
  
## Tipos de resultado  
 DT_R8  
  
## Comentários  
 A *expressão numérica* é convertida para o tipo de dados DT_R8 antes de o logaritmo ser computado. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Se *numeric_expression* for avaliado como zero ou um valor negativo, o resultado de retorno será nulo.  
  
## Exemplos de expressões  
 Esse exemplo usa um literal numérico. A função retorna o valor 1.988291341907488.  
  
```  
LOG(97.34)  
```  
  
 Esse exemplo usa a coluna **Length**. Se o valor da coluna for 101.24, a função retornará 2.005352136486217.  
  
```  
LOG(Length)   
```  
  
 Esse exemplo usa a variável **Length**. A variável deve ter um tipo de dados numérico ou a expressão deve incluir uma conversão explícita para um tipo de dados [!INCLUDE[ssIS](../../includes/ssis-md.md)] numérico. Se **Length** for 234.567, a função retornará 2.370266913465859.  
  
```  
LOG(@Length)   
```  
  
## Consulte também  
 [EXP &#40;Expressão SSIS&#41;](../../integration-services/expressions/exp-ssis-expression.md)   
 [LN &#40;Expressão SSIS&#41;](../../integration-services/expressions/ln-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  