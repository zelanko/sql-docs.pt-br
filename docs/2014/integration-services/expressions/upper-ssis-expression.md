---
title: UPPER (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 278a85ddce309f276f61603961169529ffcdfe67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896338"
---
# <a name="upper-ssis-expression"></a>UPPER (Expressão SSIS)
  Retorna uma expressão de caractere depois de converter caracteres minúsculos em maiúsculos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere para converter para caracteres maiúsculos.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
 UPPER só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de UPPER executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](cast-ssis-expression.md).  
  
 UPPER retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo converte um literal de cadeia de caracteres para caracteres maiúsculos. O resultado de retorno é "Hello".  
  
```  
UPPER("hello")  
```  
  
 Este exemplo converte o primeiro caractere na coluna **FirstName** para um caractere maiúsculo. Se **FirstName** for anna, o resultado de retorno será "A". Para obter mais informações, consulte [SUBSTRING &#40;Expressão do SSIS&#41;](substring-ssis-expression.md).  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 Este exemplo converte o valor na variável **PostalCode** escrever em caracteres de letra maiúscula. Se **PostalCode** for k4b1s2, o resultado de retorno será "K4B1S2".  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>Consulte também  
 [LOWER &#40;Expressão SSIS&#41;](lower-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
