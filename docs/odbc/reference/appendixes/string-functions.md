---
title: Funções de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03f783cbc287d9c315844e1a9df53187e4e2ba28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914041"
---
# <a name="string-functions"></a>Funções de cadeia de caracteres
A tabela a seguir lista as funções de manipulação de cadeia de caracteres. Um aplicativo pode determinar quais funções de cadeia de caracteres são suportadas por um driver chamando **SQLGetInfo** com um *tipo de informação* de SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Remarks  
 Argumentos denotado como *string_exp* pode ser o nome de uma coluna, um *literal de cadeia de caracteres*, ou o resultado de outra função escalar, onde o tipo de dados pode ser representado como SQL_CHAR, SQL _ VARCHAR ou SQL_LONGVARCHAR.  
  
 Argumentos denotado como *character_exp* são uma cadeia de caracteres de comprimento variável.  
  
 Argumentos denotado como *iniciar*, *comprimento*, ou *contagem* pode ser um *literal numérico* ou o resultado de outra função escalar, onde o tipo de dados subjacente pode ser representado como SQL_TINYINT, SQL_SMALLINT ou SQL_INTEGER.  
  
 As funções de cadeia de caracteres listadas aqui são baseados em 1; ou seja, o primeiro caractere na cadeia de caracteres é o caractere de 1.  
  
 As funções escalares de cadeia de caracteres do função BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH e posição foram adicionadas no ODBC 3.0 para se alinhar com o SQL-92.  
  
|Função|Description|  
|--------------|-----------------|  
|**ASCII (** *string_exp* **)** (ODBC 1.0)|Retorna o valor do código ASCII do caractere mais à esquerda do *string_exp* como um inteiro.|  
|**Função BIT_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em bits da expressão de cadeia de caracteres.<br /><br /> Não funciona apenas para tipos de dados de cadeia de caracteres, portanto não implicitamente será convert *string_exp* a cadeia de caracteres em vez disso, mas retornará o tamanho (interno) de qualquer tipo de dados é fornecido.|  
|**CHAR (** *código* **)** (ODBC 1.0)|Retorna o caractere que tem o ASCII de valor especificado pelo código *código*. O valor de *código* deve estar entre 0 e 255; caso contrário, o valor de retorno é – dependente da fonte de dados.|  
|**CHAR_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em caracteres da expressão de cadeia de caracteres, se a expressão de cadeia de caracteres é de um tipo de dados de caractere; Caso contrário, retorna o comprimento em bytes da expressão de cadeia de caracteres (o menor número inteiro não é menor que o número de bits dividido por 8). (Essa função é o mesmo que a função CHARACTER_LENGTH).|  
|**CHARACTER_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em caracteres da expressão de cadeia de caracteres, se a expressão de cadeia de caracteres é de um tipo de dados de caractere; Caso contrário, retorna o comprimento em bytes da expressão de cadeia de caracteres (o menor número inteiro não é menor que o número de bits dividido por 8). (Essa função é o mesmo que a função CHAR_LENGTH).|  
|**CONCAT (** *string_exp1*,*string_exp2 *)** (ODBC 1.0)|Retorna uma cadeia de caracteres que é o resultado da concatenação *string_exp2* para *string_exp1*. A cadeia de caracteres resultante é dependente de DBMS. Por exemplo, se a coluna representada por *string_exp1* continha um valor NULL, DB2 deve retornar nulo mas do SQL Server retornaria a cadeia de caracteres não nula.|  
|**DIFERENÇA (** *string_exp1*,*string_exp2 *)** (ODBC 2.0)|Retorna um valor inteiro que indica a diferença entre os valores retornados pela função SOUNDEX *string_exp1* e *string_exp2*.|  
|**Inserir (** *string_exp1*, *iniciar*, *comprimento*, *string_exp2 *)** (ODBC 1.0)|Retorna um caractere da cadeia de caracteres onde *comprimento* caracteres foram excluídos do *string_exp1*, começando em *iniciar*e onde *string_exp2* foi inserido na *string_exp,* começando no *iniciar*.|  
|**LCASE (** *string_exp* **)** (ODBC 1.0)|Retorna uma cadeia de caracteres igual de *string_exp*, com todas as letras maiusculas caracteres convertidos em minúsculos.|  
|**ESQUERDA (** *string_exp*, *contagem *)** (ODBC 1.0)|Retorna o mais à esquerda *contagem* caracteres de *string_exp*.|  
|**COMPRIMENTO (** *string_exp* **)** (ODBC 1.0)|Retorna o número de caracteres em *string_exp,* excluindo espaços em branco à direita.<br /><br /> **COMPRIMENTO** só aceita cadeias de caracteres. Portanto, será possível converter implicitamente *string_exp* para uma cadeia de caracteres e retornar o comprimento da cadeia de caracteres (não o tamanho interno do tipo de dados).|  
|**Localizar (** *string_exp1*, *string_exp2*[, *iniciar*]**)** (ODBC 1.0)|Retorna a posição inicial da primeira ocorrência de *string_exp1* em *string_exp2*. A pesquisa para a primeira ocorrência de *string_exp1* começa com a posição do primeiro caractere em *string_exp2* , a menos que o argumento opcional, *iniciar*, é especificado. Se *iniciar* for especificado, a pesquisa começa com a posição do caractere indicada pelo valor de *iniciar*. A primeira posição do caractere em *string_exp2* é indicado pelo valor 1. Se *string_exp1* não foi encontrado em *string_exp2*, o valor 0 será retornado.<br /><br /> Se um aplicativo pode chamar a função escalar localizar com o *string_exp1*, *string_exp2*, e *iniciar* argumentos, o driver retorna SQL_FN_STR_LOCATE quando  **SQLGetInfo** é chamado com um *opção* de SQL_STRING_FUNCTIONS. Se o aplicativo pode chamar a função escalar localizar somente com o *string_exp1* e *string_exp2* argumentos, o driver retorna SQL_FN_STR_LOCATE_2 quando **SQLGetInfo**é chamado com um *opção* de SQL_STRING_FUNCTIONS. Drivers que oferecem suporte a chamar a função de localizar com dois ou três argumentos retornam SQL_FN_STR_LOCATE e SQL_FN_STR_LOCATE_2.|  
|**LTRIM (** *string_exp* **)** (ODBC 1.0)|Retorna os caracteres do *string_exp*, com os espaços em branco removidos.|  
|**OCTET_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em bytes da expressão de cadeia de caracteres. O resultado é o menor número inteiro, não menos que o número de bits dividido por 8.<br /><br /> Não funciona apenas para tipos de dados de cadeia de caracteres, portanto não implicitamente será convert *string_exp* a cadeia de caracteres em vez disso, mas retornará o tamanho (interno) de qualquer tipo de dados é fornecido.|  
|**POSIÇÃO (** *character_exp* **na** *character_exp *)** (ODBC 3.0)|Retorna a posição da primeira expressão de caractere na segunda expressão de caractere. O resultado é um numérico exato com uma precisão de implementação definida e uma escala de 0.|  
|**Repetir (** *string_exp,* *contagem *)** (ODBC 1.0)|Retorna uma cadeia de caracteres composta de *string_exp* repetido *contagem* vezes.|  
|**Substituir (** *string_exp1*, *string_exp2*, *string_exp3 *)** (ODBC 1.0)|Pesquisa *string_exp1* foroccurrences de *string_exp2*e substitua *string_exp3*.|  
|**RIGHT (** *string_exp*, *contagem *)** (ODBC 1.0)|Retorna o mais à direita *contagem* caracteres de *string_exp*.|  
|**RTRIM (** *string_exp* **)** (ODBC 1.0)|Retorna os caracteres do *string_exp* com à direita de espaços em branco removidos.|  
|**SOUNDEX (** *string_exp* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres de origem dependente de dados que representa o som das palavras na *string_exp*. Por exemplo, o SQL Server retorna um código SOUNDEX de 4 dígitos; Oracle retorna uma representação fonética de cada palavra.|  
|**ESPAÇO (** *contagem* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres que consiste em *contagem* espaços.|  
|**SUBSTRING (** *string_exp*, *iniciar*, comprimento **)** (ODBC 1.0)|Retorna uma cadeia de caracteres que é derivada de *string_exp*, começando na posição do caractere especificada por *iniciar* para *comprimento* caracteres.|  
|**UCASE (** *string_exp* **)** (ODBC 1.0)|Retorna uma cadeia de caracteres igual de *string_exp*, com todos os caracteres convertidos em letras maiusculas de minúsculas.|
