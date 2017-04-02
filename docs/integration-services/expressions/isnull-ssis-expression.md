---
title: "ISNULL (Express&#227;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "valores nulos [Integration Services]"
  - "função ISNULL"
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# ISNULL (Express&#227;o SSIS)
  Retorna um resultado booliano, baseando-se em se uma expressão é nula.  
  
## Sintaxe  
  
```  
  
ISNULL(expression)  
```  
  
## Argumentos  
 *expressão*  
 É uma expressão válida de qualquer tipo de dados.  
  
## Tipos de resultado  
 DT_BOOL  
  
## Exemplos de expressões  
 Este exemplo retornará TRUE se a coluna **DiscontinuedDate** contiver um valor nulo.  
  
```  
ISNULL(DiscontinuedDate)  
```  
  
 Este exemplo retornará "Sobrenome desconhecido" se o valor na coluna **LastName** for nulo; caso contrário ele retornará o valor em **LastName**.  
  
```  
ISNULL(LastName)? "Unknown last name":LastName  
```  
  
 Este exemplo sempre retorna TRUE se a coluna **DaysToManufacture** for nula, independentemente do valor da variável **AddDays**.  
  
```  
ISNULL(DaysToManufacture + @AddDays)  
```  
  
## Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  