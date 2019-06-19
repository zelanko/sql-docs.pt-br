---
title: SUBSTRING (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SUBSTRING function
- part of expression returned [Integration Services]
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 991ef48e2b4cef24eba5034f07d5545e01198e5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724999"
---
# <a name="substring-ssis-expression"></a>SUBSTRING (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Retorna a parte de uma expressão de caractere que inicia na posição especificada e tem o comprimento especificado. O parâmetro *position* e o parâmetro *length* devem ser avaliados como inteiros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SUBSTRING(character_expression, position, length)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere da qual extrair caracteres.  
  
 *position*  
 É um inteiro que especifica onde a subcadeia de caracteres começa.  
  
 *length*  
 É um inteiro que especifica o comprimento da subcadeia de caracteres como o número de caracteres.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 SUBSTRING usa um único índice. Se *position* for 1, a subcadeia de caracteres começará com o primeiro caractere em *character_expression*.  
  
 SUBSTRING só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes que SUBSTRING execute sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 SUBSTRING retorna um resultado nulo se o argumento for nulo.  
  
 Todos os argumentos na expressão podem usar variáveis e colunas.  
  
 O argumento *length* pode exceder o comprimento da cadeia de caracteres. Naquele caso, a função retorna o restante da cadeia de caracteres.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna dois caracteres, começando com o caractere 4, de uma literal de cadeia de caracteres. O resultado de retorno é "ph".  
  
```  
SUBSTRING("elephant",4,2)  
```  
  
 Este exemplo retorna o restante de uma literal de cadeia de caracteres, começando no quarto caractere. O resultado de retorno é "phant". Isso não é um erro para o argumento *length* exceder o comprimento da cadeia de caracteres.  
  
```  
SUBSTRING ("elephant",4,50)  
```  
  
 Este exemplo retorna a primeira letra da coluna **MiddleName** .  
  
```  
SUBSTRING(MiddleName,1,1)  
```  
  
 Este exemplo usa variáveis nos argumentos *position* e *length* . Se **Start** for 1 e **Length** for 5, a função retornará os primeiros cinco caracteres na coluna **Name** .  
  
```  
SUBSTRING(Name,@Start,@Length)  
```  
  
 Este exemplo retorna os últimos quatro caracteres da variável **PostalCode** começando no sexto caractere.  
  
```  
SUBSTRING (@PostalCode,6,4)  
```  
  
 Este exemplo retorna uma cadeia de caracteres de comprimento zero de uma literal de cadeia de caracteres.  
  
```  
SUBSTRING ("Redmond",4,0)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
