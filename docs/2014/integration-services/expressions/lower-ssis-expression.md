---
title: LOWER (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1468e205f6d7a368b9b4af2a693fd369e11af233
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050061"
---
# <a name="lower-ssis-expression"></a>LOWER (Expressão SSIS)
  Retorna uma expressão character depois de converter caracteres maiúsculos em minúsculos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere para converter para caracteres minúsculos.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
 LOWER só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de LOWER executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](cast-ssis-expression.md).  
  
 LOWER retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo converte um literal de cadeia de caracteres para caracteres minúsculos. O resultado de retorno é "Nova Iorque".  
  
```  
LOWER("New York")  
```  
  
 Este exemplo converte todos os caracteres da coluna de entrada **Color** , exceto o primeiro caractere, para caracteres minúsculos. Se Color for AMARELO, o resultado de retorno será "Amarelo". Para obter mais informações, consulte [SUBSTRING &#40;Expressão do SSIS&#41;](substring-ssis-expression.md).  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 Este exemplo converte o valor na variável **CityName** para caracteres minúsculos.  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>Consulte também  
 [SUPERIOR &#40;expressão do SSIS&#41;](upper-ssis-expression.md)   
 [Funções &#40;expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
