---
title: RIGHT (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RIGHT function
ms.assetid: 83e70e75-4be5-4783-a8cf-032f82afe16e
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fecf460a9a3b1b05bf0cf221a1f037e0bf780c9b
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404288"
---
# <a name="right-ssis-expression"></a>RIGHT (Expressão SSIS)
  Retorna o número especificado de caracteres da parte mais à direita da expressão character especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RIGHT(character_expression,integer_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere da qual extrair caracteres.  
  
 *integer_expression*  
 É uma expressão de inteiro que indica o número de caracteres retornados.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 Se *integer_expression* for maior que o comprimento de *character_expression*, a função retornará *character_expression*.  
  
 Se *integer_expression* for zero, a função retornará uma cadeia de comprimento zero.  
  
 Se *integer_expression* for um número negativo, a função retornará um erro.  
  
 O argumento *integer_expression* pode assumir variáveis e colunas.  
  
 RIGHT só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes que RIGHT execute sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 RIGHT retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 O exemplo a seguir usa um literal de cadeia de caracteres. O resultado de retorno é `"Bike"`.  
  
```  
RIGHT("Mountain Bike", 4)  
```  
  
 Este exemplo retorna o número dos caracteres na extrema direita que são especificados na variável `Times` , da coluna `Name` . Se `Name` for `Touring Front Wheel` e `Times` for 5, o resultado de retorno será `"Wheel"`.  
  
```  
RIGHT(Name, @Times)  
```  
  
 Este exemplo a seguir retorna o número dos caracteres na extrema direita que são especificados na variável `Times` , da coluna `Name` . `Times` tem um tipo de dados não inteiro e a expressão inclui uma conversão explícita para o tipo de dados DT_I2. Se `Name` for `Touring Front Wheel` e `Times` for `4.32`, o resultado de retorno será `"heel"` porque a função RIGHT converterá o valor de 4.32 para 4, e então retornará os quatro caracteres na extrema direita.  
  
```  
RIGHT(Name, (DT_I2)@Times))  
```  
  
## <a name="see-also"></a>Consulte Também  
 [LEFT &#40;Expressão SSIS&#41;](../../integration-services/expressions/left-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
