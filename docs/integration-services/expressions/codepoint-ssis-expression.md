---
title: "CODEPOINT (Expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43a96940ba28fc76ae271ff0f10b2b3177635346
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="codepoint-ssis-expression"></a>CODEPOINT (Expressão SSIS)
  Retorna o ponto de código Unicode do caractere da extrema esquerda de uma expressão de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caracteres cujo caractere da extrema esquerda será avaliado.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_UI2  
  
## <a name="remarks"></a>Remarks  
 *character_expression* deve ter o tipo de dados DT_WSTR.  
  
 CODEPOINT retornará um resultado nulo se *character_expression* for nulo ou uma cadeia de caracteres vazia.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo usa um literal de cadeia de caracteres. O resultado de retorno é 77, o ponto de código Unicode para M.  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 Este exemplo usa uma variável. Se **Name** for Roda Dianteira de Passeio, o resultado de retorno será 84, o ponto de código de Unicode para T.  
  
```  
CODEPOINT(@Name)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
