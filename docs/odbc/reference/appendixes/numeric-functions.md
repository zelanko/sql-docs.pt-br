---
title: Funções Numéricas | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03da5b6644e0f7df3dc4e5e16a211cb503023bad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299866"
---
# <a name="numeric-functions"></a>Funções numéricas
A tabela a seguir descreve funções numéricas incluídas no conjunto de funções escalares ODBC. Ao ligar para **o SQLGetInfo** com um tipo de *informação* de SQL_NUMERIC_FUNCTIONS, um aplicativo pode determinar quais funções numéricas são suportadas por um driver.  
  
 Todas as funções numéricas retornam valores do tipo de dados SQL_FLOAT exceto abs, ROUND, TRUNCATE, SIGN, FLOOR e CEILING, que retornam valores do mesmo tipo de dados que os parâmetros de entrada.  
  
 Argumentos denotados como *numeric_exp* podem ser o nome de uma coluna, o resultado de outra função escalar, ou um *numérico-litera*l, onde o tipo de dados subjacente poderia ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL ou SQL_DOUBLE.  
  
 Argumentos denotados como *float_exp* podem ser o nome de uma coluna, o resultado de outra função escalar, ou um *numérico-literal,* onde o tipo de dados subjacente pode ser representado como SQL_FLOAT.  
  
 Argumentos denotados como *integer_exp* podem ser o nome de uma coluna, o resultado de outra função escalar, ou um *numérico-literal,* onde o tipo de dados subjacente pode ser representado como SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER ou SQL_BIGINT.  
  
 As funções CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP escalar foram adicionadas no ODBC 3.0 para se alinhar em SQL-92.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**ABS** _(numeric_exp)_ **)** (ODBC 1.0)|Devolve o valor absoluto de *numeric_exp*.|  
|**ACOS** _(float_exp)_ **)** (ODBC 1.0)|Retorna o arcocosino de *float_exp* como um ângulo, expresso em radianos.|  
|**ASIN** _(float_exp)_ **)** (ODBC 1.0)|Retorna o arco de *float_exp* como um ângulo, expresso em radianos.|  
|**ATAN** _(float_exp)_ **)** (ODBC 1.0)|Retorna o arcotangente de *float_exp* como um ângulo, expresso em radianos.|  
|**ATAN2 (** _float_exp1_, _float_exp2_**)** (ODBC 2.0)|Retorna o arcotangente das coordenadas *x* e *y,* especificados por *float_exp1* e *float_exp2,* respectivamente, como ângulo, expressos em radianos.|  
|**TETO** _(numeric_exp)_ **)** (ODBC 1.0)|Retorna o menor inteiro maior ou igual a *numeric_exp*. O valor de retorno é do mesmo tipo de dados do parâmetro de entrada.|  
|**COS** _(float_exp)_ **)** (ODBC 1.0)|Retorna o cosseno de *float_exp,* onde *float_exp* é um ângulo expresso em radianos.|  
|**COT** _(float_exp)_ **)** (ODBC 1.0)|Retorna o cotangente de *float_exp,* onde *float_exp* é um ângulo expresso em radianos.|  
|**GRAUS** _(numeric_exp)_ **)** (ODBC 2.0)|Retorna o número de graus convertidos de *numeric_exp* radianos.|  
|**EXP** _(float_exp)_ **)** (ODBC 1.0)|Retorna o valor exponencial de *float_exp*.|  
|**FLOOR(** _(numeric_exp)_ **)** (ODBC 1.0)|Retorna o maior inteiro menor ou igual a *numeric_exp*. O valor de retorno é do mesmo tipo de dados do parâmetro de entrada.|  
|**LOG** _(float_exp)_ **)** (ODBC 1.0)|Retorna o logaritmo natural de *float_exp.*|  
|**LOG10** _(float_exp)_ **)** (ODBC 2.0)|Retorna a base 10 logaritmo de *float_exp*.|  
|**MOD (** _integer_exp1_, _integer_exp2_**)** (ODBC 1.0)|Devolve o restante (módulo) de *integer_exp1* dividido por *integer_exp2*.|  
|**PI( )** (ODBC 1.0)|Retorna o valor constante de pi como um valor de ponto flutuante.|  
|**(numeric_exp,** _numeric_exp_ _integer_exp_**)** (ODBC 2.0)|Devolve o valor de *numeric_exp* ao poder de *integer_exp*.|  
|**RADIANS** _(numeric_exp)_ **)** (ODBC 2.0)|Retorna o número de radianos convertidos de *numeric_exp* graus.|  
|**RAND***(integer_exp)*(ODBC 1.0)**)**|Retorna um valor de ponto flutuante aleatório usando *integer_exp* como o valor opcional da semente.|  
|**ROUND(** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|O *retorno numeric_exp* arredondado para *integer_exp* lugares direito do ponto decimal. Se *integer_exp* for negativo, *numeric_exp* é arredondado para &#124;*integer_exp*&#124; lugares à esquerda do ponto decimal.|  
|**SIGN(** _numeric_exp_ **)** (ODBC 1.0)|Retorna um indicador do sinal de *numeric_exp*. Se *numeric_exp* for menor que zero, -1 é devolvido. Se *numeric_exp* igual a zero, 0 é devolvido. Se *numeric_exp* for maior que zero, 1 é devolvido.|  
|**SIN(float_exp)** _float_exp_ **)** (ODBC 1.0)|Retorna o seno de *float_exp,* onde *float_exp* é um ângulo expresso em radianos.|  
|**SQRT** _(float_exp)_ **)** (ODBC 1.0)|Retorna a raiz quadrada de *float_exp*.|  
|**TAN** _(float_exp)_ **)** (ODBC 1.0)|Retorna a tangente de *float_exp,* onde *float_exp* é um ângulo expresso em radianos.|  
|**TRUNCATE** _(numeric_exp,_ _integer_exp)_**)** (ODBC 2.0)|Retorna *numeric_exp* truncado para *integer_exp* lugares direito do ponto decimal. Se *integer_exp* for negativo, *numeric_exp* é truncado para &#124;*integer_exp*&#124; lugares à esquerda do ponto decimal.|
