---
title: "EXP (Express&#227;o SSIS) | Microsoft Docs"
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
  - "funções exponenciais"
  - "função EXP"
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# EXP (Express&#227;o SSIS)
  Retorna o expoente para a base e de uma expressão numérica. A função EXP complementa a ação da função LN e, às vezes, é chamado de antilogaritmo.  
  
## Sintaxe  
  
```  
  
EXP(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida.  
  
## Tipos de resultado  
 DT_R8  
  
## Comentários  
 A expressão numérica é lançada para o tipo de dados de DT_R8 antes de o expoente ser computado. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 O resultado de retorno sempre é um número positivo.  
  
## Exemplos de expressões  
 Estes exemplos se aplicam à função EXP para valores positivo e negativos e para zero.  
  
```  
EXP(74)  
```  
  
 Retorna 1.373382979540176E+32.  
  
```  
EXP(-27)  
```  
  
 Retorna 1.879528816539083E-12.  
  
```  
EXP(0)  
```  
  
 Retorna 1.  
  
## Consulte também  
 [LOG &#40;Expressão SSIS&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  