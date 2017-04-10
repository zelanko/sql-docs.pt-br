---
title: "ROUND (Express&#227;o SSIS) | Microsoft Docs"
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
  - "arredondando expressões"
  - "função ROUND [SSIS]"
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# ROUND (Express&#227;o SSIS)
  Retorna uma expressão numérica arredondada ao comprimento ou precisão especificados. O parâmetro de comprimento deve ser avaliado como um inteiro.  
  
## Sintaxe  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## Argumentos  
 *numeric_expression*  
 É uma expressão de um tipo de numérico válido. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *comprimento*  
 É uma expressão de inteiro. Precisão para a qual *numeric_expression* é arredondada.  
  
## Tipos de resultado  
 O mesmo tipo que *numeric*_*expression.*  
  
## Comentários  
 O argumento *length* deve ser avaliado como um inteiro positivo ou zero.  
  
 ROUND retornará um resultado nulo se o argumento for nulo.  
  
## Exemplos de expressões  
 Estes exemplos arredondam literais numéricos para um comprimento de três. O primeiro resultado de retorno é 137.1570, o segundo em 137.1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  