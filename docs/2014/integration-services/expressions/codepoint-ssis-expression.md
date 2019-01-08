---
title: CODEPOINT (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a625a4168fd5d9e7ecfa414d21298f0df3dcb396
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811498"
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
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
