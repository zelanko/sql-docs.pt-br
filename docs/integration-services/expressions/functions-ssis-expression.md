---
title: Funções (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 38729c2588ce7f779951403e72470b5ab0744e14
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816934"
---
# <a name="functions-ssis-expression"></a>Funções (Expressão SSIS)
  A linguagem de expressão inclui um conjunto de funções a ser usado em expressões. Uma expressão pode usar uma única função, mas normalmente uma expressão combina funções com operadores e usa várias funções.  
  
 As funções podem ser classificadas nos seguintes grupos:  
  
-   As funções matemáticas que executam cálculos com base em valores de entrada numéricos fornecidos como parâmetros para as funções e retornam valores numéricos.  
  
-   As funções de cadeia que executam operações em cadeia de caracteres ou em valores de entrada hexadecimais e retornam uma cadeia de caracteres ou um valor numérico.  
  
-   As funções de data e hora que executam operações em valores de data e hora e retornam valores de cadeia de caracteres, numéricos ou de data e hora.  
  
-   As funções do sistema que retornam informações sobre uma expressão.  
  
 A linguagem da expressão fornece as seguintes funções matemáticas.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[ABS &#40;Expressão SSIS&#41;](../../integration-services/expressions/abs-ssis-expression.md)|Retorna o valor positivo absoluto de uma expressão numérica.|  
|[EXP &#40;Expressão SSIS&#41;](../../integration-services/expressions/exp-ssis-expression.md)|Retorna o exponente para base e da expressão especificada.|  
|[CEILING &#40;Expressão do SSIS&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)|Retorna o menor inteiro que é maior que ou igual a uma expressão numérica.|  
|[FLOOR &#40;Expressão SSIS&#41;](../../integration-services/expressions/floor-ssis-expression.md)|Retorna o maior inteiro que é menor que ou igual a uma expressão numérica.|  
|[LN &#40;Expressão SSIS&#41;](../../integration-services/expressions/ln-ssis-expression.md)|Retorna o logaritmo natural de uma expressão numérica.|  
|[LOG &#40;Expressão SSIS&#41;](../../integration-services/expressions/log-ssis-expression.md)|Retorna o logaritmo de base 10 de uma expressão numérica.|  
|[POWER &#40;Expressão SSIS&#41;](../../integration-services/expressions/power-ssis-expression.md)|Retorna o resultado da elevação de uma expressão numérica a uma potência.|  
|[ROUND &#40;Expressão SSIS&#41;](../../integration-services/expressions/round-ssis-expression.md)|Retorna uma expressão numérica arredondada ao comprimento ou precisão especificados. para obter informações sobre a ferramenta de configuração e recursos adicionais.|  
|[SIGN &#40;Expressão SSIS&#41;](../../integration-services/expressions/sign-ssis-expression.md)|Retorna o sinal positivo (+), negativo (-) ou zero (0) de uma expressão numérica.|  
|[SQUARE &#40;Expressão SSIS&#41;](../../integration-services/expressions/square-ssis-expression.md)|Retorna o quadrado de uma expressão numérica.|  
|[SQRT &#40;Expressão SSIS&#41;](../../integration-services/expressions/sqrt-ssis-expression.md)|Retorna a raiz quadrada de uma expressão numérica.|  
  
 O avaliador da expressão fornece as seguintes funções de cadeia de caracteres.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[CODEPOINT &#40;Expressão SSIS&#41;](../../integration-services/expressions/codepoint-ssis-expression.md)|Retorna o valor do código Unicode do caractere da extrema esquerda de uma expressão de caractere.|  
|[FINDSTRING &#40;Expressão SSIS&#41;](../../integration-services/expressions/findstring-ssis-expression.md)|Retorna o índice de base um da ocorrência especificada de uma cadeia de caracteres em uma expressão.|  
|[HEX &#40;Expressão SSIS&#41;](../../integration-services/expressions/hex-ssis-expression.md)|Retorna uma cadeia de caracteres que representa o valor hexadecimal de um inteiro.|  
|[LEN &#40;Expressão SSIS&#41;](../../integration-services/expressions/len-ssis-expression.md)|Retorna o número de caracteres em uma expressão character.|  
|[LEFT &#40;Expressão SSIS&#41;](../../integration-services/expressions/left-ssis-expression.md)|Retorna o número especificado de caracteres da parte mais à esquerda da expressão character especificada.|  
|[LOWER &#40;Expressão SSIS&#41;](../../integration-services/expressions/lower-ssis-expression.md)|Retorna uma expressão character depois de converter caracteres maiúsculos em minúsculos.|  
|[LTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)|Retorna uma expressão de caractere depois de remover espaços em branco à esquerda.|  
|[REPLACE &#40;Expressão SSIS&#41;](../../integration-services/expressions/replace-ssis-expression.md)|Retorna uma expressão de caractere depois de substituir uma cadeia na expressão por uma cadeia diferente ou vazia.|  
|[REPLICATE &#40;Expressão SSIS&#41;](../../integration-services/expressions/replicate-ssis-expression.md)|Retorna uma expressão character, replicada um número especificado de vezes.|  
|[REVERSE &#40;Expressão SSIS&#41;](../../integration-services/expressions/reverse-ssis-expression.md)|Retorna uma expressão character na ordem inversa.|  
|[RIGHT &#40;Expressão SSIS&#41;](../../integration-services/expressions/right-ssis-expression.md)|Retorna o número especificado de caracteres da parte mais à direita da expressão character especificada.|  
|[RTRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)|Retorna uma expressão character depois de remover espaços em branco à direita.|  
|[SUBSTRING &#40;Expressão SSIS&#41;](../../integration-services/expressions/substring-ssis-expression.md)|Retorna uma parte de uma expressão de caractere.|  
|[TRIM &#40;Expressão SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md)|Retorna uma expressão de caractere depois de remover espaços em branco à esquerda e direita.|  
|[UPPER &#40;Expressão do SSIS&#41;](../../integration-services/expressions/upper-ssis-expression.md)|Retorna uma expressão de caractere depois de converter caracteres minúsculos em maiúsculos.|  
  
 O avaliador de expressão fornce as seguintes funções de data e hora.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[DATEADD &#40;Expressão do SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)|Retorna um novo valor DT_DBTIMESTAMP adicionando um intervalo de data ou hora a uma data especificada.|  
|[DATEDIFF &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)|Retorna o número de limites de data e hora entre duas datas especificadas.|  
|[DATEPART &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)|Retorna um inteiro que representa uma parte de uma data.|  
|[DAY &#40;Expressão do SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)|Retorna um inteiro que representa o dia da data especificada.|  
|[GETDATE &#40;Expressão do SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md)|Retorna a data atual do sistema.|  
|[GETUTCDATE &#40;Expressão do SSIS&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)|Retorna a data atual do sistema na hora UTC (Universal Time Coordinate ou Greenwich Mean Time).|  
|[MONTH &#40;Expressão do SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)|Retorna um inteiro que representa o mês da data especificada.|  
|[YEAR &#40;Expressão do SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)|Retorna um inteiro que representa o ano da data especificada.|  
  
 O avaliador da expressão fornece as seguintes funções nulas.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[ISNULL &#40;Expressão SSIS&#41;](../../integration-services/expressions/isnull-ssis-expression.md)|Retorna um resultado booliano, baseando-se em se uma expressão é nula.|  
|[NULL &#40;Expressão SSIS&#41;](../../integration-services/expressions/null-ssis-expression.md)|Retorna um valor nulo de um tipo de dados solicitado.|  
  
 São mostrados nomes de expressão em caracteres maiúsculos, mas os nomes de expressão não fazem distinção entre maiúsculas e minúsculas. Por exemplo, usando trabalhos "nulos" assim como "NULOS".  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)   
 [Exemplos de expressões avançadas do Integration Services](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
