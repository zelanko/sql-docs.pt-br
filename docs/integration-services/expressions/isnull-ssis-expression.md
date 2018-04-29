---
title: ISNULL (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b311a59b7245c18782e1faed6eac5a4b4af31020
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="isnull-ssis-expression"></a>ISNULL (Expressão SSIS)
  Retorna um resultado booliano, baseando-se em se uma expressão é nula.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ISNULL(expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É uma expressão válida de qualquer tipo de dados.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="expression-examples"></a>Exemplos de expressões  
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
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  
