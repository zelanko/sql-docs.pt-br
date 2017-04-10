---
title: "SIGN (Express&#227;o SSIS) | Microsoft Docs"
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
  - "valores positivos [Integration Services]"
  - "função SIGN"
  - "valores negativos"
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# SIGN (Express&#227;o SSIS)
  Retorna o sinal positivo (+1), negativo (-1) ou zero (0) de uma expressão numérica.  
  
## Sintaxe  
  
```  
  
SIGN(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 É uma expressão numérica assinada válida. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Tipos de resultado  
 DT_I4  
  
## Comentários  
 SIGN retornará um resultado nulo se o argumento for nulo.  
  
## Exemplos de expressões  
 Este exemplo retorna o sinal de um literal numérico. O resultado de retorno é -1.  
  
```  
SIGN(-123.45)  
```  
  
 Este exemplo retorna o sinal do resultado da subtração da coluna **StandardCost** da coluna **DealerPrice** .  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  