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
manager: craigg
ms.openlocfilehash: c0eeccf4e9c972592f8efecb622fc71f4f3c87a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720050"
---
# <a name="string-functions"></a>Funções de cadeia de caracteres
A tabela a seguir lista as funções de manipulação de cadeia de caracteres. Um aplicativo pode determinar quais funções de cadeia de caracteres são suportadas por um driver chamando **SQLGetInfo** com um *tipo de informação* de SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Comentários  
 Argumentos denotado como *string_exp* pode ser o nome de uma coluna, um *literal de cadeia de caracteres*, ou o resultado de outra função escalar, onde o tipo de dados subjacente pode ser representado como SQL_CHAR, SQL _ VARCHAR ou SQL_LONGVARCHAR.  
  
 Argumentos denotado como *character_exp* são uma cadeia de caracteres de comprimento variável.  
  
 Argumentos denotado como *inicie*, *comprimento*, ou *contagem* pode ser uma *literal numérico* ou o resultado de outra função escalar, onde o tipo de dados subjacente pode ser representado como SQL_TINYINT, SQL_SMALLINT ou SQL_INTEGER.  
  
 As funções de cadeia de caracteres listadas aqui são baseados em 1; ou seja, o primeiro caractere na cadeia de caracteres é o caractere de 1.  
  
 As funções escalares de cadeia de caracteres do função BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, função OCTET_LENGTH e posição foram adicionadas no ODBC 3.0 para se alinhar com o SQL-92.  
  
|Função|Description|  
|--------------|-----------------|  
|**ASCII (** *string_exp* **)** (ODBC 1.0)|Retorna o valor do código ASCII do caractere mais à esquerda do *string_exp* como um número inteiro.|  
|**Função BIT_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em bits da expressão de cadeia de caracteres.<br /><br /> Não funcionam apenas para tipos de dados de cadeia de caracteres, portanto será implicitamente não converter *string_exp* a cadeia de caracteres, mas em vez disso, retornará o tamanho (interno) de qualquer tipo de dados é fornecido.|  
|**CHAR (** *código* **)** (ODBC 1.0)|Retorna o caractere que tem o ASCII de valor especificado pelo código *código*. O valor de *código* deve estar entre 0 e 255; caso contrário, o valor retornado é dependente da fonte de dados.|  
|**CHAR_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em caracteres da expressão de cadeia de caracteres, se a expressão de cadeia de caracteres é de um tipo de dados de caractere; Caso contrário, retorna o comprimento em bytes da expressão de cadeia de caracteres (o menor inteiro não menor do que o número de bits dividido por 8). (Essa função é o mesmo que a função CHARACTER_LENGTH).|  
|**CHARACTER_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em caracteres da expressão de cadeia de caracteres, se a expressão de cadeia de caracteres é de um tipo de dados de caractere; Caso contrário, retorna o comprimento em bytes da expressão de cadeia de caracteres (o menor inteiro não menor do que o número de bits dividido por 8). (Essa função é o mesmo que a função CHAR_LENGTH).|  
|**CONCAT (** *string_exp1*,*string_exp2 com * * *)** (ODBC 1.0)|Retorna uma cadeia de caracteres que é o resultado da concatenação *string_exp2 com* à *string_exp1*. A cadeia de caracteres resultante é dependente de DBMS. Por exemplo, se a coluna representada por *string_exp1* continha um valor NULL, DB2 retorno nulo mas do SQL Server seria retornaria a cadeia de caracteres não-nulo.|  
|**DIFERENÇA (** *string_exp1*,*string_exp2 com * * *)** (ODBC 2.0)|Retorna um valor inteiro que indica a diferença entre os valores retornados pela função SOUNDEX para *string_exp1* e *string_exp2 com*.|  
|**INSERT (** *string_exp1*, *iniciar*, *comprimento*, *string_exp2 com * * *)** (ODBC 1.0)|Retorna um caractere de cadeia de caracteres onde *comprimento* caracteres tenham sido excluídos do *string_exp1*, começando no *iniciar*e onde *string_exp2 com* foi inserido na *string_exp,* começando no *iniciar*.|  
|**LCASE (** *string_exp* **)** (ODBC 1.0)|Retorna uma cadeia de caracteres igual ao que, na *string_exp*, com todas as letras maiusculas caracteres convertidos em minúsculos.|  
|**ESQUERDA (** *string_exp*, *contagem * * *)** (ODBC 1.0)|Retorna o mais à esquerda *contagem* caracteres de *string_exp*.|  
|**COMPRIMENTO (** *string_exp* **)** (ODBC 1.0)|Retorna o número de caracteres em *string_exp,* excluindo espaços em branco à direita.<br /><br /> **COMPRIMENTO** só aceita cadeias de caracteres. Portanto converterá implicitamente *string_exp* para uma cadeia de caracteres e retornar o comprimento da cadeia de caracteres (não o tamanho interno do tipo de dados).|  
|**Localizar (** *string_exp1*, *string_exp2 com*[, *iniciar*]**)** (ODBC 1.0)|Retorna a posição inicial da primeira ocorrência de *string_exp1* dentro *string_exp2 com*. A pesquisa a primeira ocorrência de *string_exp1* começa com a posição do primeiro caractere no *string_exp2 com* , a menos que o argumento opcional, *iniciar*, é especificado. Se *inicie* for especificado, a pesquisa começa com a posição de caractere indicada pelo valor de *iniciar*. A primeira posição do caractere em *string_exp2 com* é indicado pelo valor de 1. Se *string_exp1* não for encontrada na *string_exp2 com*, o valor 0 será retornado.<br /><br /> Se um aplicativo pode chamar a função escalar de localização com o *string_exp1*, *string_exp2 com*, e *iniciar* argumentos, o driver retorna SQL_FN_STR_LOCATE quando  **SQLGetInfo** é chamado com um *opção* de SQL_STRING_FUNCTIONS. Se o aplicativo pode chamar a função escalar de localizar apenas com o *string_exp1* e *string_exp2 com* argumentos, o driver retorna SQL_FN_STR_LOCATE_2 quando **SQLGetInfo**é chamado com um *opção* de SQL_STRING_FUNCTIONS. Drivers que dão suporte ao chamar a função de localizar com dois ou três argumentos retornam SQL_FN_STR_LOCATE e SQL_FN_STR_LOCATE_2.|  
|**LTRIM (** *string_exp* **)** (ODBC 1.0)|Retorna os caracteres de *string_exp*, com os principais espaços em branco removidos.|  
|**Função OCTET_LENGTH (** *string_exp* **)** (ODBC 3.0)|Retorna o comprimento em bytes da expressão de cadeia de caracteres. O resultado é o menor número inteiro, não menos que o número de bits dividido por 8.<br /><br /> Não funcionam apenas para tipos de dados de cadeia de caracteres, portanto será implicitamente não converter *string_exp* a cadeia de caracteres, mas em vez disso, retornará o tamanho (interno) de qualquer tipo de dados é fornecido.|  
|**POSIÇÃO (** *character_exp* **IN** *character_exp * * *)** (ODBC 3.0)|Retorna a posição da primeira expressão de caractere na segunda expressão de caractere. O resultado é um valor numérico exato com uma precisão de definido pela implementação e uma escala de 0.|  
|**Repetir (** *string_exp,* *contagem * * *)** (ODBC 1.0)|Retorna uma cadeia de caracteres composta *string_exp* repetido *contagem* vezes.|  
|**Substituir (** *string_exp1*, *string_exp2 com*, *string_exp3 * * *)** (ODBC 1.0)|Pesquisa *string_exp1* foroccurrences de *string_exp2 com*e substitua *string_exp3*.|  
|**DIREITA (** *string_exp*, *contagem * * *)** (ODBC 1.0)|Retorna o mais à direita *contagem* caracteres de *string_exp*.|  
|**RTRIM (** *string_exp* **)** (ODBC 1.0)|Retorna os caracteres de *string_exp* com à direita de espaços em branco removidos.|  
|**SOUNDEX (** *string_exp* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres de dependente da fonte de dados que representa o som das palavras nos *string_exp*. Por exemplo, o SQL Server retorna um código SOUNDEX de 4 dígitos; Oracle retorna uma representação fonética de cada palavra.|  
|**ESPAÇO (** *contagem* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres consistindo *contagem* espaços.|  
|**Subcadeia de caracteres (** *string_exp*, *iniciar*, comprimento **)** (ODBC 1.0)|Retorna uma cadeia de caracteres que é derivada de *string_exp*, começando na posição do caractere especificada por *inicie* para *comprimento* caracteres.|  
|**UCASE (** *string_exp* **)** (ODBC 1.0)|Retorna uma cadeia de caracteres igual ao que, na *string_exp*, com todos os caracteres convertidos em letras maiusculas de minúsculas.|
