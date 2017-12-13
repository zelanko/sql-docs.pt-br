---
title: "FINDSTRING (Expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FINDSTRING function
ms.assetid: c83cb1b1-3c52-4496-b518-4c9253b9336d
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fe1b65f8df06863490757513bd4520ee9ed925cf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="findstring-ssis-expression"></a>FINDSTRING (Expressão SSIS)
  Retorna o local da ocorrência especificada de uma cadeia de caracteres dentro de uma expressão de caractere. O resultado de retorno é o índice da ocorrência. O parâmetro de cadeia de caracteres deve ser avaliado como uma expressão de caractere e o parâmetro de ocorrência deve ser avaliado como um inteiro. Se a cadeia de caracteres não for localizada, o valor de retorno será 0. Se a cadeia de caracteres acontecer menos vezes que o argumento de ocorrência especifica, o valor de retorno será 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FINDSTRING(character_expression, searchstring, occurrence)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É a cadeia de caracteres para pesquisa.  
  
 *searchstring*  
 É a cadeia de caracteres para pesquisa.  
  
 *ocorrência*  
 É um inteiro com sinal ou sem sinal que especifica qual ocorrência de *searchstring* deve ser informada.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 FINDSTRING funciona apenas com o tipo de dados DT_WSTR.  Os argumentos*character_expression* e *searchstring* , que são literais de cadeia de caracteres ou colunas de dados com o tipo de dados DT_STR, são implicitamente convertidos para o tipo de dados DT_WSTR antes de FINDSTRING executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;Expressão SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 FINDSTRING retornará nulo se *character_expression* ou *searchstring* forem nulos.  
  
 Use um valor de 1 no argumento *occurrence* para obter o índice da primeira ocorrência, 2 para a segunda ocorrência e assim por diante.  
  
 A *occurrence* deve ser um inteiro com um valor maior do que 0.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo usa um literal de cadeia de caracteres. Retorna o valor 11.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 1)   
```  
  
 Este exemplo usa um literal de cadeia de caracteres. Porque a cadeia de caracteres "NY" ocorre só duas vezes, o resultado de retorno é 0.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 3)   
```  
  
 Este exemplo usa a coluna **Name** . Ele retorna o local do valor n na coluna **Name** . O resultado de retorno varia, dependendo do valor em **Name**. Se **Name** contiver Anderson, a função retornará 8.  
  
```  
FINDSTRING(Name,"n", 2)   
```  
  
 Este exemplo usa as colunas **Name** e **Size** . Retorna o local do caractere na extrema esquerda do valor **Size** na coluna **Name** . O resultado de retorno varia, dependendo de valores de coluna. Se **Name** contiver Mountain,500Red,42 e **Size** contiver 42, o resultado de retorno será 17.  
  
```  
FINDSTRING(Name,Size,1)   
```  
  
## <a name="see-also"></a>Consulte também  
 [REPLACE &#40;Expressão SSIS&#41;](../../integration-services/expressions/replace-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
