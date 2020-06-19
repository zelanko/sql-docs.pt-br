---
title: TOKENCOUNT (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c0efed1-c2b3-4f20-a3a1-ad91283b7c0a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: df34c21e200f5a9f4a9242a3280913acf14adf76
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968967"
---
# <a name="tokencount-ssis-expression"></a>TOKENCOUNT (expressão SSIS)
  Retorna o número de tokens em uma cadeia de caracteres que contém tokens separados pelos delimitadores especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TOKENCOUNT(character_expression, delimiter_string)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Uma cadeia de caracteres que contém tokens separados por delimitadores.  
  
 *delimiter_string*  
 Uma cadeia de caracteres que contém caracteres delimitadores. Por exemplo, "; ," contém três caracteres delimitadores ponto e vírgula, um espaço em branco e uma vírgula.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 Os comentários a seguir se aplicam à função TOKEN:  
  
-   A cadeia de caracteres delimitadores pode conter um ou mais caracteres delimitadores.  
  
-   Delimitadores à esquerda são ignorados.  
  
-   TOKENCOUNT funciona apenas com o tipo de dados DT_WSTR. Um argumento *character_expression* que é um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR é implicitamente convertido no tipo de dados DT_WSTR antes de TOKEN executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR.  
  
-   TOKENCOUNT retornará 0 (zero) se o character_expression for nulo.  
  
-   É possível usar variáveis e colunas como argumentos para essa expressão.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 No exemplo a seguir, a função TOKENCOUNT retorna 3 porque a cadeia de caracteres contém três tokens: "01", "12", "2011".  
  
```  
TOKENCOUNT("01/12/2011", "/")  
```  
  
 No exemplo a seguir, a função TOKENCOUNT retorna 4 porque há quatro tokens ("a", "little", "white", "dog").  
  
```  
TOKENCOUNT("a little white dog"," ")  
```  
  
 No exemplo a seguir, a função TOKENCOUNT retorna 1. A função analisa a cadeia de caracteres de entrada para verificar se há delimitadores e, como não há, ela adiciona a cadeia de caracteres inteira como o primeiro token.  
  
```  
TOKENCOUNT("a little white dog","|")  
```  
  
 No exemplo a seguir, a função TOKENCOUNT retorna 4. A cadeia de caracteres delimitadores neste exemplo contém cinco delimitadores. A cadeia de caracteres de entrada contém quatro tokens: "a", "little", "white", "dog".  
  
```  
TOKENCOUNT("a:little|white dog","| ,.:")  
```  
  
 No exemplo a seguir, a função TOKENCOUNT retorna 4. Ela ignora todos os caracteres de espaço à esquerda.  
  
```  
TOKENCOUNT("        a little white dog", " ")  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
