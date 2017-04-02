---
title: "SQRT (Express&#227;o SSIS) | Microsoft Docs"
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
  - "função SQRT"
  - "raiz quadrada de determinada expressão"
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# SQRT (Express&#227;o SSIS)
  Retorna a raiz quadrada de uma expressão numérica.  
  
## Sintaxe  
  
```  
  
SQRT(numeric_expression)  
```  
  
## Argumentos  
 *numeric_expression*  
 É uma expressão numérica de qualquer tipo de dados numérico. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Tipos de resultado  
 DT_R8  
  
## Comentários  
 SQRT retornará um resultado nulo se o argumento for nulo.  
  
 SQRT falhará se o argumento for um valor negativo.  
  
 O argumento é convertido para o tipo de dados de DT_R8 antes da operação de raiz quadrada.  
  
## Exemplos de expressões  
 Este exemplo retorna a raiz quadrada de um literal numérico. O resultado de retorno é 12.  
  
```  
SQRT(144)  
```  
  
 Este exemplo retorna a raiz quadrada de uma expressão, o resultado da subtração de valores nas colunas **Value1** e **Value2** .  
  
```  
SQRT(Value1 - Value2)  
```  
  
 Este exemplo retorna o comprimento do terceiro lado de um triângulo direito, aplicando a função SQUARE a duas variáveis e calculando, em seguida, a raiz quadrada da soma. Se **Side1** contiver 3 e **Side2** contiver 4, a função SQRT retornará 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  Em expressões, nomes de variável incluem sempre o prefixo @.  
  
## Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  