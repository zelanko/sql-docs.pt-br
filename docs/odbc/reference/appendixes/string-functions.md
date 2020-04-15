---
title: Funções de corda | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9323809028ad170a4811b1af8b6e276cdbb4293
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302837"
---
# <a name="string-functions"></a>Funções de Cadeia de Caracteres
A tabela a seguir lista funções de manipulação de strings. Um aplicativo pode determinar quais funções de string são suportadas por um driver ligando para **sqlgetinfo** com um tipo de *informação* de SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Comentários  
 Argumentos denotados como *string_exp* podem ser o nome de uma coluna, um *caractere-string-literal*, ou o resultado de outra função escalar, onde o tipo de dados subjacente pode ser representado como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR.  
  
 Os argumentos denotados como *character_exp* são uma seqüência de caracteres de comprimento variável.  
  
 Argumentos denotados como *início,* *comprimento*ou *contagem* podem ser *um numérico-literal* ou o resultado de outra função escalar, onde o tipo de dados subjacente pode ser representado como SQL_TINYINT, SQL_SMALLINT ou SQL_INTEGER.  
  
 As funções de string listadas aqui são baseadas em 1; ou seja, o primeiro personagem da seqüência é o personagem 1.  
  
 As funções escalares de seqüência de BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH e POSITION foram adicionadas no ODBC 3.0 para se alinhar em SQL-92.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**ASCII** _(string_exp)_ **)** (ODBC 1.0)|Retorna o valor de código ASCII do caractere mais à esquerda de *string_exp* como um inteiro.|  
|**BIT_LENGTH** _(string_exp)_ **)** (ODBC 3.0)|Retorna o comprimento em bits da expressão de cadeia de caracteres.<br /><br /> Não funciona apenas para tipos de dados de seqüência, portanto, não converterá implicitamente *string_exp* em string, mas, em vez disso, retornará o tamanho (interno) de qualquer tipo de dados que for dado.|  
|**CHAR** _(código)_ **)** (ODBC 1.0)|Retorna o caractere que tem o valor de código ASCII especificado por *código*. O valor do *código* deve ser entre 0 e 255; caso contrário, o valor de retorno é dependente da fonte de dados.|  
|**CHAR_LENGTH(string_exp)** _string_exp_ **)** (ODBC 3.0)|Retorna o comprimento em caracteres da expressão string, se a expressão de string for de um tipo de dados de caracteres; caso contrário, retorna o comprimento em bytes da expressão de corda (o menor inteiro não menos do que o número de bits dividido por 8). (Esta função é a mesma que a função CHARACTER_LENGTH.)|  
|**CHARACTER_LENGTH** _(string_exp)_ **)** (ODBC 3.0)|Retorna o comprimento em caracteres da expressão string, se a expressão de string for de um tipo de dados de caracteres; caso contrário, retorna o comprimento em bytes da expressão de corda (o menor inteiro não menos do que o número de bits dividido por 8). (Esta função é a mesma que a função CHAR_LENGTH.)|  
|**CONCAT (** _string_exp1_,_string_exp2_**)** (ODBC 1.0)|Retorna uma seqüência de caracteres que é o resultado da concatenação *string_exp2* para *string_exp1*. A cadeia de caracteres resultante é dependente de DBMS. Por exemplo, se a coluna representada por *string_exp1* contivesse um valor NULO, o DB2 retornaria NULL, mas o SQL Server retornaria a seqüência não-NULL.|  
|**DIFERENÇA (** _string_exp1_,_string_exp2_**)** (ODBC 2.0)|Retorna um valor inteiro que indica a diferença entre os valores retornados pela função SOUNDEX para *string_exp1* e *string_exp2*.|  
|**INSERIR** _(string_exp1,_ *iniciar,* *comprimento,* _string_exp2)_**)** (ODBC 1.0)|Retorna uma seqüência de caracteres onde os caracteres de *comprimento* foram excluídos de *string_exp1*, começando no *início*, e onde *string_exp2* foi inserido em *string_exp,* a partir do *início*.|  
|**LCASE** _(string_exp)_ **)** (ODBC 1.0)|Retorna uma seqüência igual à que em *string_exp,* com todos os caracteres maiúsculos convertidos em minúsculas.|  
|**ESQUERDA (** _string_exp_, _contagem_**)** (ODBC 1.0)|Retorna os caracteres de *contagem* mais à esquerda de *string_exp*.|  
|**COMPRIMENTO (string_exp** _string_exp_ **)** (ODBC 1.0)|Retorna o número de caracteres em *string_exp,* excluindo espaços em branco.<br /><br /> **LENGTH** só aceita strings. Portanto, converterá implicitamente *string_exp* em uma string e retornará o comprimento desta string (não o tamanho interno do tipo de dados).|  
|**LOCALIZAÇÃO (** _string_exp1_, *string_exp2*[, *start]***)** (ODBC 1.0)|Retorna a posição inicial da primeira ocorrência de *string_exp1* dentro *de string_exp2*. A busca pela primeira ocorrência de *string_exp1* começa com a primeira posição de caractere em *string_exp2,* a menos que o argumento opcional, *comece,* seja especificado. Se *o início* for especificado, a pesquisa começará com a posição de caractere indicada pelo valor de *início*. A primeira posição de caractere em *string_exp2* é indicada pelo valor 1. Caso *string_exp1* não seja encontrado dentro *string_exp2,* o valor 0 é devolvido.<br /><br /> Se um aplicativo pode chamar a função LOCATE scalar com os *argumentos string_exp1*, *string_exp2*e *iniciar,* o driver retorna SQL_FN_STR_LOCATE quando **o SQLGetInfo** é chamado com uma *opção* de SQL_STRING_FUNCTIONS. Se o aplicativo puder chamar a função ESCALADOR LOCALIZAR apenas com os argumentos *string_exp1* e *string_exp2,* o driver retorna SQL_FN_STR_LOCATE_2 quando **o SQLGetInfo** for chamado com uma *opção* de SQL_STRING_FUNCTIONS. Os drivers que suportam a chamada da função LOCATE com dois ou três argumentos retornam SQL_FN_STR_LOCATE e SQL_FN_STR_LOCATE_2.|  
|**LTRIM** _(string_exp)_ **)** (ODBC 1.0)|Retorna os caracteres de *string_exp,* com os principais espaços em branco removidos.|  
|**OCTET_LENGTH** _(string_exp)_ **)** (ODBC 3.0)|Retorna o comprimento em bytes da expressão de cadeia de caracteres. O resultado é o menor número inteiro, não menos que o número de bits dividido por 8.<br /><br /> Não funciona apenas para tipos de dados de seqüência, portanto, não converterá implicitamente *string_exp* em string, mas, em vez disso, retornará o tamanho (interno) de qualquer tipo de dados que for dado.|  
|**POSIÇÃO (** _character_exp_ **EM** _character_exp_**)** (ODBC 3.0)|Retorna a posição da primeira expressão de caractere na expressão do segundo caractere. O resultado é um numérico exato com uma precisão definida pela implementação e uma escala de 0.|  
|**REPEAT** _(string_exp,_ _contagem)_**)** (ODBC 1.0)|Retorna uma seqüência de caracteres composta de *string_exp* repetidos tempos *de contagem.*|  
|**REPLACE (** _string_exp1_, *string_exp2*, _string_exp3_**)** (ODBC 1.0)|Procure *string_exp1* de ocorrências de *string_exp2*e substitua por *string_exp3*.|  
|**RIGHT (** _string_exp_, _contagem_**)** (ODBC 1.0)|Retorna os caracteres de *contagem* mais à direita de *string_exp*.|  
|**RTRIM** _(string_exp)_ **)** (ODBC 1.0)|Retorna os caracteres de *string_exp* com espaços em branco removidos.|  
|**SOUNDEX** _(string_exp)_ **)** (ODBC 2.0)|Retorna uma seqüência de caracteres dependente da fonte de dados representando o som das palavras em *string_exp*. Por exemplo, o SQL Server retorna um código SOUNDEX de 4 dígitos; Oracle retorna uma representação fonética de cada palavra.|  
|**ESPAÇO** _(contagem)_ **)** (ODBC 2.0)|Retorna uma seqüência de caracteres que consiste em espaços de *contagem.*|  
|**SUBSTRING (string_exp** _string_exp_, *início,* comprimento **)** (ODBC 1.0)|Retorna uma seqüência de caracteres derivada de *string_exp*, começando na posição de caractere especificada por *iniciar* para caracteres *de comprimento.*|  
|**UCASE** _(string_exp)_ **)** (ODBC 1.0)|Retorna uma seqüência igual à que em *string_exp,* com todos os caracteres minúsculos convertidos em maiúsculas.|
