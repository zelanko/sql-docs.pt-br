---
title: LOWER (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bea0342ef01511621629559cb627447d66340071
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725209"
---
# <a name="lower-ssis-expression"></a>LOWER (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>Remarks  
 LOWER só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de LOWER executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LOWER retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo converte um literal de cadeia de caracteres para caracteres minúsculos. O resultado de retorno é "Nova Iorque".  
  
```  
LOWER("New York")  
```  
  
 Este exemplo converte todos os caracteres da coluna de entrada **Color** , exceto o primeiro caractere, para caracteres minúsculos. Se Color for AMARELO, o resultado de retorno será "Amarelo". Para obter mais informações, consulte [SUBSTRING &#40;Expressão do SSIS&#41;](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 Este exemplo converte o valor na variável **CityName** para caracteres minúsculos.  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [UPPER &#40;Expressão do SSIS&#41;](../../integration-services/expressions/upper-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
