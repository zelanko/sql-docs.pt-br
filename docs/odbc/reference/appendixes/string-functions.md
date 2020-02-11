---
title: Funções de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd4ec3e05acfd4faaafd38a79e48c67d03d86bd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070171"
---
# <a name="string-functions"></a>Funções de Cadeia de Caracteres
A tabela a seguir lista as funções de manipulação de cadeia de caracteres. Um aplicativo pode determinar quais funções de cadeia de caracteres têm suporte por um driver chamando **SQLGetInfo** com um *tipo de informação* de SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Comentários  
 Argumentos denotados como *string_exp* podem ser o nome de uma coluna, um *literal de cadeia de caracteres*ou o resultado de outra função escalar, em que o tipo de dados subjacente pode ser representado como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR.  
  
 Argumentos indicados como *character_exp* são uma cadeia de caracteres de comprimento variável.  
  
 Os argumentos denotados como *início*, *comprimento*ou *contagem* podem ser um *literal numérico* ou o resultado de outra função escalar, em que o tipo de dados subjacente pode ser representado como SQL_TINYINT, SQL_SMALLINT ou SQL_INTEGER.  
  
 As funções de cadeia de caracteres listadas aqui são baseadas em 1; ou seja, o primeiro caractere na cadeia de caracteres é o caractere 1.  
  
 As funções escalares BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH e posição de cadeia de caracteres foram adicionadas no ODBC 3,0 para serem alinhadas com o SQL-92.  
  
|Função|DESCRIÇÃO|  
|--------------|-----------------|  
|**ASCII (** _string_exp_ **)** (ODBC 1,0)|Retorna o valor do código ASCII do caractere da extrema esquerda de *string_exp* como um inteiro.|  
|**BIT_LENGTH (** _string_exp_ **)** (ODBC 3,0)|Retorna o comprimento em bits da expressão de cadeia de caracteres.<br /><br /> Não funciona apenas para tipos de dados de cadeia de caracteres, portanto, não converterá implicitamente *string_exp* em cadeia de caracteres, mas, em vez disso, retornará o tamanho (interno) de qualquer tipo de dados que for fornecido.|  
|**Char (** _Code_ **)** (ODBC 1,0)|Retorna o caractere que tem o valor de código ASCII especificado pelo *código*. O valor do *código* deve estar entre 0 e 255; caso contrário, o valor de retorno será dependente da fonte de dados.|  
|**CHAR_LENGTH (** _string_exp_ **)** (ODBC 3,0)|Retorna o comprimento em caracteres da expressão de cadeia de caracteres, se a expressão de cadeia de caracteres for de um tipo de dados de caractere; caso contrário, retorna o comprimento em bytes da expressão de cadeia de caracteres (o menor inteiro não menor que o número de bits dividido por 8). (Essa função é a mesma que a função CHARACTER_LENGTH.)|  
|**CHARACTER_LENGTH (** _string_exp_ **)** (ODBC 3,0)|Retorna o comprimento em caracteres da expressão de cadeia de caracteres, se a expressão de cadeia de caracteres for de um tipo de dados de caractere; caso contrário, retorna o comprimento em bytes da expressão de cadeia de caracteres (o menor inteiro não menor que o número de bits dividido por 8). (Essa função é a mesma que a função CHAR_LENGTH.)|  
|**Concat (** _string_exp1_,_string_exp2_**)** (ODBC 1,0)|Retorna uma cadeia de caracteres que é o resultado da concatenação de *string_exp2* para *string_exp1*. A cadeia de caracteres resultante é dependente de DBMS. Por exemplo, se a coluna representada por *string_exp1* contiver um valor nulo, o DB2 retornará nulo, mas SQL Server retornará a cadeia de caracteres não nula.|  
|**Diferença (** _string_exp1_,_string_exp2_**)** (ODBC 2,0)|Retorna um valor inteiro que indica a diferença entre os valores retornados pela função SOUNDEX para *string_exp1* e *string_exp2*.|  
|**Insert (** _string_exp1_, *início*, *comprimento*, _string_exp2_**)** (ODBC 1,0)|Retorna uma cadeia de caracteres em que os caracteres de *comprimento* foram excluídos da *string_exp1*, começando no *início*e onde *string_exp2* foi inserido no *string_exp,* começando no *início*.|  
|**LCase (** _string_exp_ **)** (ODBC 1,0)|Retorna uma cadeia de caracteres igual a em *string_exp*, com todos os caracteres maiúsculos convertidos em minúsculas.|  
|**Esquerda (** _string_exp_, _contagem_**)** (ODBC 1,0)|Retorna os caracteres de *contagem* mais à esquerda de *string_exp*.|  
|**Comprimento (** _string_exp_ **)** (ODBC 1,0)|Retorna o número de caracteres em *string_exp,* excluindo os espaços em branco à direita.<br /><br /> **Comprimento** só aceita cadeias de caracteres. Portanto, o converterá implicitamente *string_exp* em uma cadeia de caracteres e retornará o comprimento dessa cadeia de caracteres (não o tamanho interno do tipo de dados).|  
|**Localizar (** _string_exp1_, *string_exp2*[, *Iniciar*]**)** (ODBC 1,0)|Retorna a posição inicial da primeira ocorrência de *string_exp1* em *string_exp2*. A pesquisa pela primeira ocorrência de *string_exp1* começa com a primeira posição de caractere em *string_exp2* , a menos que o argumento opcional, *Start*, seja especificado. Se *Start* for especificado, a pesquisa começará com a posição de caractere indicada pelo valor de *Start*. A primeira posição de caractere em *string_exp2* é indicada pelo valor 1. Se *string_exp1* não for encontrado no *string_exp2*, o valor 0 será retornado.<br /><br /> Se um aplicativo puder chamar a função localizar escalar com os argumentos *string_exp1*, *string_exp2*e *iniciar* , o driver retornará SQL_FN_STR_LOCATE quando **SQLGetInfo** for chamado com uma *opção* de SQL_STRING_FUNCTIONS. Se o aplicativo puder chamar a função localizar escalar apenas com os argumentos *string_exp1* e *string_exp2* , o driver retornará SQL_FN_STR_LOCATE_2 quando **SQLGetInfo** for chamado com uma *opção* de SQL_STRING_FUNCTIONS. Os drivers que dão suporte à chamada da função localizar com dois ou três argumentos retornam SQL_FN_STR_LOCATE e SQL_FN_STR_LOCATE_2.|  
|**LTRIM (** _string_exp_ **)** (ODBC 1,0)|Retorna os caracteres de *string_exp*, com espaços em branco à esquerda removidos.|  
|**OCTET_LENGTH (** _string_exp_ **)** (ODBC 3,0)|Retorna o comprimento em bytes da expressão de cadeia de caracteres. O resultado é o menor número inteiro, não menos que o número de bits dividido por 8.<br /><br /> Não funciona apenas para tipos de dados de cadeia de caracteres, portanto, não converterá implicitamente *string_exp* em cadeia de caracteres, mas, em vez disso, retornará o tamanho (interno) de qualquer tipo de dados que for fornecido.|  
|**Position (** _character_exp_ **em** _character_exp_**)** (ODBC 3,0)|Retorna a posição da primeira expressão de caractere na segunda expressão de caractere. O resultado é um numeric exato com uma precisão definida pela implementação e uma escala de 0.|  
|**Repetir (** _string_exp,_ _contagem_**)** (ODBC 1,0)|Retorna uma cadeia de caracteres composta de *string_exp* tempos de *contagem* repetidos.|  
|**Replace (** _string_exp1_, *string_exp2*, _string_exp3_**)** (ODBC 1,0)|Pesquise *string_exp1* foroccurrences de *string_exp2*e substitua por *string_exp3*.|  
|**Direita (** _string_exp_, _contagem_**)** (ODBC 1,0)|Retorna os caracteres de *contagem* mais à direita de *string_exp*.|  
|**Rtrim (** _string_exp_ **)** (ODBC 1,0)|Retorna os caracteres de *string_exp* com espaços em branco à direita removidos.|  
|**SOUNDEX (** _string_exp_ **)** (ODBC 2,0)|Retorna uma cadeia de caracteres dependente da fonte de dados que representa o som das palavras em *string_exp*. Por exemplo, SQL Server retorna um código SOUNDEX de 4 dígitos; O Oracle retorna uma representação fonética de cada palavra.|  
|**Espaço (** _contagem_ **)** (ODBC 2,0)|Retorna uma cadeia de caracteres que consiste em espaços de *contagem* .|  
|**Subcadeia de caracteres (** _string_exp_, *início*, comprimento **)** (ODBC 1,0)|Retorna uma cadeia de caracteres que é derivada de *string_exp*, começando na posição do caractere especificada pelo *início* para caracteres de *comprimento* .|  
|**UCase (** _string_exp_ **)** (ODBC 1,0)|Retorna uma cadeia de caracteres igual a em *string_exp*, com todos os caracteres minúsculos convertidos em letras maiúsculas.|
