---
title: "CODEPOINT (expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: af56c3de2d4e285960b9e6631084b20440396eb3
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

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
  
## <a name="remarks"></a>Comentários  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40; Expressão do SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

