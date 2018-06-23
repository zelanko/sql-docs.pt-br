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
ms.topic: article
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e25fcb18b0224780e3dff2fcbe62b88f8a3d0322
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012057"
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
 [DIREITA &#40;expressão SSIS&#41;](right-ssis-expression.md)   
 [Funções &#40;expressão SSIS&#41;](functions-ssis-expression.md)  
  
  