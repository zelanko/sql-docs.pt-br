---
title: ISNULL (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 51eda21b5c9b85c5f9cfd613d0d92df9729fe620
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428463"
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
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/coalesce-transact-sql)  
  
  
