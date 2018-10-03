---
title: Funções numéricas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca33d451fe5e1431d9bc4fb29196b98adcfb933f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620364"
---
# <a name="numeric-functions"></a>Funções numéricas
A tabela a seguir descreve as funções numéricas que estão incluídas no conjunto de função escalar ODBC. Chamando **SQLGetInfo** com um *tipo de informação* de SQL_NUMERIC_FUNCTIONS, um aplicativo pode determinar quais funções numéricas são suportadas por um driver.  
  
 Todas as funções numéricas retornam valores de tipo de dados SQL_FLOAT exceto ABS, ROUND, TRUNCATE, entrada, FLOOR e CEILING, que retornam valores dos mesmos dados de tipo como os parâmetros de entrada.  
  
 Argumentos denotado como *numeric_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *litera numérico*l, onde o tipo de dados poderia ser representado como SQL_NUMERIC, SQL _ DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL ou SQL_DOUBLE.  
  
 Argumentos denotado como *float_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *literal numérico*, onde o tipo de dados subjacente pode ser representado como SQL_FLOAT.  
  
 Argumentos denotado como *integer_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *literal numérico*, onde o tipo de dados subjacente pode ser representado como SQL_TINYINT, SQL _ SQL_BIGINT, SQL_INTEGER ou SMALLINT.  
  
 As funções escalares a função CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP foram adicionadas no ODBC 3.0 para se alinhar com o SQL-92.  
  
|Função|Description|  
|--------------|-----------------|  
|**ABS (** *numeric_exp* **)** (ODBC 1.0)|Retorna o valor absoluto do *numeric_exp*.|  
|**ACOS (** *float_exp* **)** (ODBC 1.0)|Retorna o arco cosseno *float_exp* como um ângulo, expresso em radianos.|  
|**ASIN (** *float_exp* **)** (ODBC 1.0)|Retorna o arco seno de *float_exp* como um ângulo, expresso em radianos.|  
|**ATAN (** *float_exp* **)** (ODBC 1.0)|Retorna o arco tangente de *float_exp* como um ângulo, expresso em radianos.|  
|**ATAN2 (** *float_exp1*, *float_exp2 * * *)** (ODBC 2.0)|Retorna o arco tangente do *x* e *y* coordenadas, especificado por *float_exp1* e *float_exp2*, respectivamente, como um ângulo expresso em radianos.|  
|**CEILING (** *numeric_exp* **)** (ODBC 1.0)|Retorna o menor inteiro maior ou igual a *numeric_exp*. O valor retornado é do mesmo tipo de dados como o parâmetro de entrada.|  
|**COS (** *float_exp* **)** (ODBC 1.0)|Retorna o cosseno *float_exp*, onde *float_exp* é um ângulo expressado em radianos.|  
|**COT (** *float_exp* **)** (ODBC 1.0)|Retorna a cotangente *float_exp*, onde *float_exp* é um ângulo expressado em radianos.|  
|**GRAUS (** *numeric_exp* **)** (ODBC 2.0)|Retorna o número de graus convertido de *numeric_exp* radianos.|  
|**EXP (** *float_exp* **)** (ODBC 1.0)|Retorna o valor exponencial da *float_exp*.|  
|**FLOOR (** *numeric_exp* **)** (ODBC 1.0)|Retorna o maior inteiro menor ou igual a *numeric_exp*. O valor retornado é do mesmo tipo de dados como o parâmetro de entrada.|  
|**LOG (** *float_exp* **)** (ODBC 1.0)|Retorna o logaritmo natural de *float_exp*.|  
|**LOG10 (** *float_exp* **)** (ODBC 2.0)|Logaritmo de base 10 de retorna de *float_exp*.|  
|**MOD (** *integer_exp1*, *integer_exp2 * * *)** (ODBC 1.0)|Retorna o resto dos *integer_exp1* dividido pelo *integer_exp2*.|  
|**(PI)** (ODBC 1.0)|Retorna o valor da constante de pi como um valor de ponto flutuante.|  
|**POWER (** *numeric_exp*, *integer_exp * * *)** (ODBC 2.0)|Retorna o valor de *numeric_exp* à potência de *integer_exp*.|  
|**RADIANOS (** *numeric_exp* **)** (ODBC 2.0)|Retorna o número de radianos convertido de *numeric_exp* graus.|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|Retorna um valor de ponto flutuante aleatório usando *integer_exp* como o valor de semente opcional.|  
|**ROUND (** *numeric_exp*, *integer_exp * * *)** (ODBC 2.0)|Retorna *numeric_exp* arredondado *integer_exp* casas à direita da vírgula decimal. Se *integer_exp* for negativo, *numeric_exp* será arredondado para &#124; *integer_exp* &#124; casas à esquerda da vírgula decimal.|  
|**ENTRADA (** *numeric_exp* **)** (ODBC 1.0)|Retorna o sinal de um indicador *numeric_exp*. Se *numeric_exp* é menor que zero, -1 será retornado. Se *numeric_exp* é igual a zero, 0 será retornado. Se *numeric_exp* é maior que zero, 1 será retornado.|  
|**SIN (** *float_exp* **)** (ODBC 1.0)|Retorna o seno *float_exp*, onde *float_exp* é um ângulo expressado em radianos.|  
|**SQRT (** *float_exp* **)** (ODBC 1.0)|Retorna a raiz quadrada de *float_exp*.|  
|**TAN (** *float_exp* **)** (ODBC 1.0)|Retorna a tangente de *float_exp*, onde *float_exp* é um ângulo expressado em radianos.|  
|**Truncar (** *numeric_exp*, *integer_exp * * *)** (ODBC 2.0)|Retorna *numeric_exp* truncados para *integer_exp* casas à direita da vírgula decimal. Se *integer_exp* for negativo, *numeric_exp* é cortada para &#124; *integer_exp* &#124; casas à esquerda da vírgula decimal.|
