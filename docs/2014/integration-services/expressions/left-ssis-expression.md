---
title: LEFT (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: da89c1a1740d8acd0f284d9cf1475d34ca651792
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252588"
---
# <a name="left-ssis-expression"></a>LEFT (Expressão SSIS)
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
  
## <a name="remarks"></a>Remarks  
 Se *number* for maior que o comprimento de *character_expression*, a função retornará *character_expression*.  
  
 Se *number* for zero, a função retornará uma cadeia de comprimento zero.  
  
 Se *number* for um número negativo, a função retornará um erro.  
  
 O argumento *number* pode obter variáveis e colunas.  
  
 LEFT só funciona com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido para o tipo de dados DT_WSTR antes de LEFT executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](cast-ssis-expression.md).  
  
 LEFT retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 O exemplo a seguir usa um literal de cadeia de caracteres. O resultado de retorno é `"Mountain"`.  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>Consulte também  
 [DIREITA &#40;expressão do SSIS&#41;](right-ssis-expression.md)   
 [Funções &#40;expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
