---
title: "ABS (Express&#227;o SSIS) | Microsoft Docs"
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
  - "função ABS"
  - "valor positivo absoluto"
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# ABS (Express&#227;o SSIS)
  Retorna o valor positivo absoluto de uma expressão numérica.  
  
## Sintaxe  
  
```  
  
ABS(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 É uma expressão numérica assinada ou não assinada.  
  
## Tipos de resultado  
 O tipo de dados da expressão numérica submetido à função.  
  
## Comentários  
 ABS retornará um resultado nulo se o argumento for nulo.  
  
## Exemplos de expressões  
 Estes exemplos se aplicam à função ABS para um número positivo e um negativo. Ambos retornam 1.23.  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 Este exemplo se aplica à função ABS para uma expressão que subtrai valores nas variáveis **HighTemperature** e **LowTempature**.  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  