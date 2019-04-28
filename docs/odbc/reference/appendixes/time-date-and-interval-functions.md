---
title: Funções de intervalo, data e hora | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1303ca724ef6790ae7bcf218ab8ed0e5da4ed38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735082"
---
# <a name="time-date-and-interval-functions"></a>Funções de hora, data e intervalo
A tabela a seguir lista as funções de data e hora que estão incluídas no conjunto de função escalar ODBC. Um aplicativo pode determinar quais funções de data e hora são suportadas por um driver chamando **SQLGetInfo** com um *tipo de informação* de SQL_TIMEDATE_FUNCTIONS.  
  
 Argumentos denotado como *timestamp_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *ODBC de tempo de escape*, *ODBC-Data-escape*, ou *Escape de carimbo de hora de ODBC*, onde o tipo de dados poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotado como *date_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *escape de ODBC-Data* ou *escape de carimbo de hora de ODBC*, em que o tipo de dados subjacente pode ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotado como *time_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *ODBC de tempo de escape* ou *escape de carimbo de hora de ODBC*, em que o tipo de dados subjacente pode ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 A função CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP timedate funções escalares foram adicionados no ODBC 3.0 para se alinhar com o SQL-92.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**(FUNÇÃO CURRENT_DATE)** (ODBC 3.0)|Retorna a data atual.|  
|**CURRENT_TIME [(** *precisão de tempo* **)]** (ODBC 3.0)|Retorna a hora local atual. O *precisão de tempo* argumento determina a precisão de segundos do valor retornado.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *timestamp precisão* **)]** (ODBC 3.0)|Retorna a data local atual e a hora local como um valor de carimbo de hora. O *precisão de carimbo de hora* argumento determina a precisão de segundos do carimbo de hora retornada.|  
|**(CURDATE)** (ODBC 1.0)|Retorna a data atual.|  
|**(FUNÇÃO CURTIME)** (ODBC 1.0)|Retorna a hora local atual.|  
|**Função DAYNAME (** *date_exp* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres que contém o nome específico de fonte de dados do dia (por exemplo, Sunday a Saturday ou Sun. a Sat. para uma fonte de dados que usa o inglês, ou Sonntag a samstag para uma fonte de dados que usa alemão) para a parte do dia *date_exp*.|  
|**Dia do mês (** *date_exp* **)** (ODBC 1.0)|Retorna o dia do mês com base no campo mês de *date_exp* como um valor inteiro no intervalo de 1 a 31.|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|Retorna o dia da semana com base no campo semana de *date_exp* como um valor inteiro no intervalo de 1 a 7, em que 1 representa domingo.|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|Retorna o dia do ano, com base em um campo ano na *date_exp* como um valor inteiro no intervalo de 1-366.|  
|**EXTRAIR (** *extrair campo FROM* *origem extração* **)** (ODBC 3.0)|Retorna o *extrair campo* parte a *origem extração*. O *origem extração* argumento é uma expressão datetime ou intervalo. O *extrair campo* argumento pode ser uma das seguintes palavras-chave:<br /><br /> ANO MÊS DIA HORA SEGUNDO UM MINUTO<br /><br /> A precisão do valor retornado é definido pela implementação. A escala é 0, a menos que o segundo for especificado, caso em que a escala não é menor que a precisão de frações do *origem extração* campo.|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|Retorna a hora com base no campo de hora *time_exp* como um valor inteiro no intervalo de 0 a 23.|  
|**MINUTO (** *time_exp* **)** (ODBC 1.0)|Retorna o minuto com base no campo minuto de *time_exp* como um valor inteiro no intervalo de 0 a 59.|  
|**MÊS (** *date_exp* **)** (ODBC 1.0)|Retorna o mês com base no campo mês de *date_exp* como um valor inteiro no intervalo de 1 a 12.|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres que contém o nome específico de fonte de dados do mês (por exemplo, janeiro a dezembro ou janeiro a dezembro para uma fonte de dados que utiliza o inglês, ou Januar a Dezember para uma fonte de dados que usa alemão) para a parte do mês *date_exp*.|  
|**AGORA ()** (ODBC 1.0)|Retorna a data e hora como um valor de carimbo de hora atual.|  
|**QUARTER(** *date_exp* **)** (ODBC 1.0)|Retorna o trimestre *date_exp* como um valor inteiro no intervalo de 1 a 4, em que 1 representa 1 de janeiro a 31 de março.|  
|**SECOND(** *time_exp* **)** (ODBC 1.0)|Retorna o segundo com base em um campo na segunda *time_exp* como um valor inteiro no intervalo de 0 a 59.|
|**TIMESTAMPADD(** *interval*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|Retorna o carimbo de hora calculado adicionando *integer_exp* intervalos do tipo *intervalo* para *timestamp_exp*. Os valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> onde os segundos fracionários são expressos em bilionésimos de segundo. Por exemplo, a instrução SQL a seguir retorna o nome de cada funcionário e sua data de aniversário de um ano:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Se *timestamp_exp* é um valor de tempo e *intervalo* Especifica os dias, semanas, meses, trimestres ou anos, a parte de data *timestamp_exp* é definido como a data atual antes de Calculando o carimbo de hora resultante.<br /><br /> Se *timestamp_exp* é um valor de data e *intervalo* Especifica fracionários segundos, segundos, minutos ou horas, a parte de hora *timestamp_exp* é definido como 0 antes de Calculando o carimbo de hora resultante.<br /><br /> Um aplicativo determina quais intervalos de uma fonte de dados oferece suporte a chamando **SQLGetInfo** com a opção SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF (** *intervalo*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Retorna o número inteiro de intervalos do tipo *intervalo* pelo qual *timestamp_exp2* é maior que *timestamp_exp1*. Os valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> onde os segundos fracionários são expressos em bilionésimos de segundo. Por exemplo, a instrução SQL a seguir retorna o nome de cada funcionário e o número de anos, que ele ou ela foi utilizada:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Se qualquer expressão de carimbo de hora for um valor de hora e *intervalo* Especifica os dias, semanas, meses, trimestres ou anos, a parte de data desse carimbo de hora é definido como a data atual antes de calcular a diferença entre os carimbos de hora.<br /><br /> Se qualquer expressão de carimbo de hora for um valor de data e *intervalo* Especifica fracionários segundos, segundos, minutos ou horas, a parte de hora desse carimbo de hora é definida como 0 antes de calcular a diferença entre os carimbos de hora.<br /><br /> Um aplicativo determina quais intervalos de uma fonte de dados oferece suporte a chamando **SQLGetInfo** com a opção SQL_TIMEDATE_DIFF_INTERVALS.|  
|**WEEK(** *date_exp* **)** (ODBC 1.0)|Retorna a semana do ano com base no campo semana de *date_exp* como um valor inteiro no intervalo de 1 a 53.|  
|**YEAR(** *date_exp* **)** (ODBC 1.0)|Retorna o ano com base em um campo ano na *date_exp* como um valor inteiro. O intervalo é dependente da fonte de dados.|
