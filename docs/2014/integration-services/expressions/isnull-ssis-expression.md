---
title: ISNULL (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6780ed81142343e0e08ff624ee80e8ef2cc532c8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129816"
---
# <a name="isnull-ssis-expression"></a>ISNULL (Expressão SSIS)
  Retorna um resultado booliano, baseando-se em se uma expressão é nula.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ISNULL(expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão*  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;expressão do SSIS&#41;](functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/coalesce-transact-sql)  
  
  
