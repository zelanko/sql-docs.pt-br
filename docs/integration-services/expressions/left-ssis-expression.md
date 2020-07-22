---
title: LEFT (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 67e83bd59e69d9113a3c95116cd2ecc590b31c4c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914522"
---
# <a name="left-ssis-expression"></a>LEFT (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Retorna o número especificado de caracteres da parte mais à esquerda da expressão character especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LEFT(character_expression,number)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma expressão de caractere da qual extrair caracteres.  
  
 *number*  
 É uma expressão de inteiro que indica o número de caracteres retornados.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentários  
 Se *number* for maior que o comprimento de *character_expression*, a função retornará *character_expression*.  
  
 Se *number* for zero, a função retornará uma cadeia de comprimento zero.  
  
 Se *number* for um número negativo, a função retornará um erro.  
  
 O argumento *number* pode obter variáveis e colunas.  
  
 LEFT só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de LEFT executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LEFT retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 O exemplo a seguir usa um literal de cadeia de caracteres. O resultado de retorno é `"Mountain"`.  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [RIGHT &#40;Expressão SSIS&#41;](../../integration-services/expressions/right-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
