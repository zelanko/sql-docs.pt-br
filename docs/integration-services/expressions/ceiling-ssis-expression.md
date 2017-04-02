---
title: "CEILING (Express&#227;o SSIS) | Microsoft Docs"
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
  - "menor número inteiro maior que ou igual à expressão"
  - "função CEILING [SSIS]"
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# CEILING (Express&#227;o SSIS)
  Retorna o menor inteiro que é maior que ou igual a uma expressão numérica.  
  
## Sintaxe  
  
```  
  
CEILING(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida.  
  
## Tipos de resultado  
 O tipo de dados da expressão numérica submetido à função.  
  
## Comentários  
 CEILING retornará um resultado nulo se o argumento for nulo.  
  
## Exemplos de expressões  
 Estes exemplos se aplicam à função CEILING para valores positivo, negativo e zero.  
  
```  
CEILING(123.74)  
```  
  
 Retorna 124,00  
  
```  
CEILING(-124.27)  
```  
  
 Retorna -124,00  
  
```  
CEILING(0.00)  
```  
  
 Retorna 0.00  
  
## Consulte também  
 [FLOOR &#40;Expressão SSIS&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  