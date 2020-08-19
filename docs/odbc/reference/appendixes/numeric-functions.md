---
description: Funções numéricas
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7575d55ad6632ffa511da32a7155ab8c4d0edf3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425018"
---
# <a name="numeric-functions"></a>Funções numéricas
A tabela a seguir descreve as funções numéricas incluídas no conjunto de funções escalares ODBC. Ao chamar **SQLGetInfo** com um *tipo de informação* de SQL_NUMERIC_FUNCTIONS, um aplicativo pode determinar quais funções numéricas são suportadas por um driver.  
  
 Todas as funções numéricas retornam valores de tipo de dados SQL_FLOAT, exceto ABS, ROUND, TRUNCATE, SIGN, FLOOR e teto, que retornam valores do mesmo tipo de dados que os parâmetros de entrada.  
  
 Argumentos denotados como *numeric_exp* podem ser o nome de uma coluna, o resultado de outra função escalar ou um *arliteral*l, em que o tipo de dados subjacente poderia ser representado como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL ou SQL_DOUBLE.  
  
 Argumentos denotados como *float_exp* podem ser o nome de uma coluna, o resultado de outra função escalar ou um *literal numérico*, onde o tipo de dados subjacente pode ser representado como SQL_FLOAT.  
  
 Argumentos denotados como *integer_exp* podem ser o nome de uma coluna, o resultado de outra função escalar ou um *literal numérico*, em que o tipo de dados subjacente pode ser representado como SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER ou SQL_BIGINT.  
  
 As funções escalares CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP foram adicionadas no ODBC 3,0 para serem alinhadas com o SQL-92.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**ABS (** _numeric_exp_ **)**  (ODBC 1,0)|Retorna o valor absoluto de *numeric_exp*.|  
|**ACOS (** _float_exp_ **)**  (ODBC 1,0)|Retorna o arco cosseno de *float_exp* como um ângulo, expresso em radianos.|  
|**Asen (** _float_exp_ **)**  (ODBC 1,0)|Retorna o arco seno de *float_exp* como um ângulo, expresso em radianos.|  
|**ATAN (** _float_exp_ **)**  (ODBC 1,0)|Retorna o arco tangente de *float_exp* como um ângulo, expresso em radianos.|  
|**ATAN2 (** _float_exp1_, _float_exp2_**)**  (ODBC 2,0)|Retorna o arco tangente das coordenadas *x* e *y* , especificado por *float_exp1* e *float_exp2*, respectivamente, como um ângulo, expresso em radianos.|  
|**Teto (** _numeric_exp_ **)**  (ODBC 1,0)|Retorna o menor inteiro maior ou igual a *numeric_exp*. O valor de retorno é do mesmo tipo de dados que o parâmetro de entrada.|  
|**Cos (** _float_exp_ **)**  (ODBC 1,0)|Retorna o cosseno de *float_exp*, onde *float_exp* é um ângulo expresso em radianos.|  
|**COT (** _float_exp_ **)**  (ODBC 1,0)|Retorna a cotangente de *float_exp*, em que *float_exp* é um ângulo expresso em radianos.|  
|**Graus (** _numeric_exp_ **)**  (ODBC 2,0)|Retorna o número de graus convertidos de *numeric_exp* radianos.|  
|**Exp (** _float_exp_ **)**  (ODBC 1,0)|Retorna o valor exponencial de *float_exp*.|  
|**Floor (** _numeric_exp_ **)**  (ODBC 1,0)|Retorna o maior número inteiro menor ou igual a *numeric_exp*. O valor de retorno é do mesmo tipo de dados que o parâmetro de entrada.|  
|**Log (** _float_exp_ **)**  (ODBC 1,0)|Retorna o logaritmo natural de *float_exp*.|  
|**Log10 (** _float_exp_ **)**  (ODBC 2,0)|Retorna o logaritmo de base 10 de *float_exp*.|  
|**Mod (** _integer_exp1_, _integer_exp2_**)**  (ODBC 1,0)|Retorna o resto (módulo) de *integer_exp1* dividido por *integer_exp2*.|  
|**PI ()**  (ODBC 1,0)|Retorna o valor constante de PI como um valor de ponto flutuante.|  
|**Power (** _numeric_exp_, _integer_exp_**)**  (ODBC 2,0)|Retorna o valor de *numeric_exp* à potência de *integer_exp*.|  
|**Radianos (** _numeric_exp_ **)**  (ODBC 2,0)|Retorna o número de radianos convertidos de *numeric_exp* graus.|  
|**Rand (**[*integer_exp*]**)**  (ODBC 1,0)|Retorna um valor de ponto flutuante aleatório usando *integer_exp* como o valor de semente opcional.|  
|**Round (** _numeric_exp_, _integer_exp_**)**  (ODBC 2,0)|Retorna *numeric_exp* arredondado para os locais de *integer_exp* à direita do ponto decimal. Se *integer_exp* for negativo, *numeric_exp* será arredondado para &#124;*integer_exp* locais&#124; à esquerda do ponto decimal.|  
|**Assinar (** _numeric_exp_ **)**  (ODBC 1,0)|Retorna um indicador do sinal de *numeric_exp*. Se *numeric_exp* for menor que zero,-1 será retornado. Se *numeric_exp* for igual a zero, 0 será retornado. Se *numeric_exp* for maior que zero, 1 será retornado.|  
|**Sin (** _float_exp_ **)**  (ODBC 1,0)|Retorna o seno de *float_exp*, onde *float_exp* é um ângulo expresso em radianos.|  
|**Sqrt (** _float_exp_ **)**  (ODBC 1,0)|Retorna a raiz quadrada de *float_exp*.|  
|**Tan (** _float_exp_ **)**  (ODBC 1,0)|Retorna a tangente de *float_exp*, em que *float_exp* é um ângulo expresso em radianos.|  
|**Truncate (** _numeric_exp_, _integer_exp_**)**  (ODBC 2,0)|Retorna *numeric_exp* truncado para os locais de *integer_exp* à direita do ponto decimal. Se *integer_exp* for negativo, *numeric_exp* será truncado para &#124;*integer_exp* locais de&#124; à esquerda do ponto decimal.|
