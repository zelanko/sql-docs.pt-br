---
title: Funções (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f70cde85aca7b08003d27ee3bd2fc61cbc0a45f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769122"
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
|[ABS &#40;Expressão SSIS&#41;](abs-ssis-expression.md)|Retorna o valor positivo absoluto de uma expressão numérica.|  
|[EXP &#40;Expressão SSIS&#41;](exp-ssis-expression.md)|Retorna o exponente para base e da expressão especificada.|  
|[CEILING &#40;Expressão do SSIS&#41;](ceiling-ssis-expression.md)|Retorna o menor inteiro que é maior que ou igual a uma expressão numérica.|  
|[FLOOR &#40;Expressão SSIS&#41;](floor-ssis-expression.md)|Retorna o maior inteiro que é menor que ou igual a uma expressão numérica.|  
|[LN &#40;Expressão SSIS&#41;](ln-ssis-expression.md)|Retorna o logaritmo natural de uma expressão numérica.|  
|[LOG &#40;Expressão SSIS&#41;](log-ssis-expression.md)|Retorna o logaritmo de base 10 de uma expressão numérica.|  
|[POWER &#40;Expressão SSIS&#41;](power-ssis-expression.md)|Retorna o resultado da elevação de uma expressão numérica a uma potência.|  
|[ROUND &#40;Expressão SSIS&#41;](round-ssis-expression.md)|Retorna uma expressão numérica arredondada ao comprimento ou precisão especificados. .|  
|[SIGN &#40;Expressão SSIS&#41;](sign-ssis-expression.md)|Retorna o sinal positivo (+), negativo (-) ou zero (0) de uma expressão numérica.|  
|[SQUARE &#40;Expressão SSIS&#41;](square-ssis-expression.md)|Retorna o quadrado de uma expressão numérica.|  
|[SQRT &#40;Expressão SSIS&#41;](sqrt-ssis-expression.md)|Retorna a raiz quadrada de uma expressão numérica.|  
  
 O avaliador da expressão fornece as seguintes funções de cadeia de caracteres.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[CODEPOINT &#40;Expressão SSIS&#41;](codepoint-ssis-expression.md)|Retorna o valor do código Unicode do caractere da extrema esquerda de uma expressão de caractere.|  
|[FINDSTRING &#40;Expressão SSIS&#41;](findstring-ssis-expression.md)|Retorna o índice de base um da ocorrência especificada de uma cadeia de caracteres em uma expressão.|  
|[HEX &#40;Expressão SSIS&#41;](hex-ssis-expression.md)|Retorna uma cadeia de caracteres que representa o valor hexadecimal de um inteiro.|  
|[LEN &#40;Expressão SSIS&#41;](len-ssis-expression.md)|Retorna o número de caracteres em uma expressão character.|  
|[LEFT &#40;Expressão SSIS&#41;](left-ssis-expression.md)|Retorna o número especificado de caracteres da parte mais à esquerda da expressão character especificada.|  
|[LOWER &#40;Expressão SSIS&#41;](lower-ssis-expression.md)|Retorna uma expressão character depois de converter caracteres maiúsculos em minúsculos.|  
|[LTRIM &#40;Expressão SSIS&#41;](trim-ssis-expression.md)|Retorna uma expressão de caractere depois de remover espaços em branco à esquerda.|  
|[REPLACE &#40;Expressão SSIS&#41;](replace-ssis-expression.md)|Retorna uma expressão de caractere depois de substituir uma cadeia na expressão por uma cadeia diferente ou vazia.|  
|[REPLICATE &#40;Expressão SSIS&#41;](replicate-ssis-expression.md)|Retorna uma expressão character, replicada um número especificado de vezes.|  
|[REVERSE &#40;Expressão SSIS&#41;](reverse-ssis-expression.md)|Retorna uma expressão character na ordem inversa.|  
|[RIGHT &#40;Expressão SSIS&#41;](right-ssis-expression.md)|Retorna o número especificado de caracteres da parte mais à direita da expressão character especificada.|  
|[RTRIM &#40;Expressão SSIS&#41;](rtrim-ssis-expression.md)|Retorna uma expressão character depois de remover espaços em branco à direita.|  
|[SUBSTRING &#40;Expressão SSIS&#41;](substring-ssis-expression.md)|Retorna uma parte de uma expressão de caractere.|  
|[TRIM &#40;Expressão SSIS&#41;](trim-ssis-expression.md)|Retorna uma expressão de caractere depois de remover espaços em branco à esquerda e direita.|  
|[UPPER &#40;Expressão do SSIS&#41;](upper-ssis-expression.md)|Retorna uma expressão de caractere depois de converter caracteres minúsculos em maiúsculos.|  
  
 O avaliador de expressão fornce as seguintes funções de data e hora.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[DATEADD &#40;Expressão do SSIS&#41;](dateadd-ssis-expression.md)|Retorna um novo valor DT_DBTIMESTAMP adicionando um intervalo de data ou hora a uma data especificada.|  
|[DATEDIFF &#40;Expressão do SSIS&#41;](datediff-ssis-expression.md)|Retorna o número de limites de data e hora entre duas datas especificadas.|  
|[DATEPART &#40;Expressão do SSIS&#41;](datepart-ssis-expression.md)|Retorna um inteiro que representa uma parte de uma data.|  
|[DAY &#40;Expressão do SSIS&#41;](day-ssis-expression.md)|Retorna um inteiro que representa o dia da data especificada.|  
|[GETDATE &#40;Expressão do SSIS&#41;](getdate-ssis-expression.md)|Retorna a data atual do sistema.|  
|[GETUTCDATE &#40;Expressão do SSIS&#41;](getutcdate-ssis-expression.md)|Retorna a data atual do sistema na hora UTC (Universal Time Coordinate ou Greenwich Mean Time).|  
|[MONTH &#40;Expressão do SSIS&#41;](month-ssis-expression.md)|Retorna um inteiro que representa o mês da data especificada.|  
|[YEAR &#40;Expressão do SSIS&#41;](year-ssis-expression.md)|Retorna um inteiro que representa o ano da data especificada.|  
  
 O avaliador da expressão fornece as seguintes funções nulas.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[ISNULL &#40;Expressão SSIS&#41;](null-ssis-expression.md)|Retorna um resultado booliano, baseando-se em se uma expressão é nula.|  
|[NULL &#40;Expressão SSIS&#41;](null-ssis-expression.md)|Retorna um valor nulo de um tipo de dados solicitado.|  
  
 São mostrados nomes de expressão em caracteres maiúsculos, mas os nomes de expressão não fazem distinção entre maiúsculas e minúsculas. Por exemplo, usando trabalhos "nulos" assim como "NULOS".  
  
## <a name="see-also"></a>Consulte também  
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)   
 [Exemplos de expressões avançadas do Integration Services](examples-of-advanced-integration-services-expressions.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](integration-services-ssis-expressions.md)  
  
  
