---
title: Funções de intervalo, data e hora | Microsoft Docs
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
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2939125046525ec73f25499f75a4b981f301615
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="time-date-and-interval-functions"></a>Funções de hora, data e intervalo
A tabela a seguir lista as funções de data e hora que são incluídas no conjunto de função escalar ODBC. Um aplicativo pode determinar quais funções de data e hora são suportadas por um driver chamando **SQLGetInfo** com um *tipo de informação* de SQL_TIMEDATE_FUNCTIONS.  
  
 Argumentos denotado como *timestamp_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *ODBC de tempo de escape*, *ODBC-Data-escape*, ou *Escape de carimbo de hora de ODBC*, onde o tipo de dados poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotado como *date_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *ODBC-Data-escape* ou *escape de carimbo de hora de ODBC*, onde o tipo de dados subjacente pode ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotado como *time_exp* pode ser o nome de uma coluna, o resultado de outra função escalar, ou um *ODBC de tempo de escape* ou *escape de carimbo de hora de ODBC*, onde o tipo de dados subjacente pode ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 CURRENT_TIMESTAMP, CURRENT_DATE e CURRENT_TIME timedate funções escalares ODBC 3.0 para se alinhar com o SQL-92 foram adicionados.  
  
|Função|Description|  
|--------------|-----------------|  
|**(CURRENT_DATE)** (ODBC 3.0)|Retorna a data atual.|  
|**CURRENT_TIME [(** *precisão de tempo* **)]** (ODBC 3.0)|Retorna a hora local atual. O *precisão de tempo* argumento determina a precisão de segundos do valor retornado.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *timestamp precisão* **)]** (ODBC 3.0)|Retorna a data local atual e a hora local como um valor de carimbo de hora. O *timestamp precisão* argumento determina a precisão de segundos do carimbo de hora retornada.|  
|**(CURDATE)** (ODBC 1.0)|Retorna a data atual.|  
|**(CURTIME)** (ODBC 1.0)|Retorna a hora local atual.|  
|**DAYNAME (** *date_exp* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres que contém o nome específico da fonte de dados do dia (por exemplo, Sunday a Saturday ou Sun. a Sat. para uma fonte de dados que usa o inglês, ou Sonntag a Samstag para uma fonte de dados que usa alemão) para a parte do dia *date_exp*.|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|Retorna o dia do mês com base no campo mês de *date_exp* como um valor inteiro no intervalo de 1 a 31.|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|Retorna o dia da semana com base no campo semana de *date_exp* como um valor inteiro no intervalo de 1 a 7, onde 1 representa domingo.|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|Retorna o dia do ano com base no campo ano de *date_exp* como um valor inteiro no intervalo de 1 a 366.|  
|**EXTRAIR (** *FROM extrair campo* *origem extração* **)** (ODBC 3.0)|Retorna o *extrair campo* parte do *origem extração*. O *origem extração* argumento é uma expressão de data e hora ou intervalo. O *extrair campo* argumento pode ser uma das seguintes palavras-chave:<br /><br /> ANO MÊS DIA HORA MINUTOS SEGUNDO<br /><br /> A precisão do valor retornado é definido pela implementação. A escala é 0, a menos que o segundo é especificado, caso em que a escala não é menor do que a precisão fracionária de segundos a *origem extração* campo.|  
|**HORA (** *time_exp* **)** (ODBC 1.0)|Retorna a hora com base no campo hora de *time_exp* como um valor inteiro no intervalo de 0 a 23.|  
|**MINUTO (** *time_exp* **)** (ODBC 1.0)|Retorna o minuto com base no campo minuto de *time_exp* como um valor inteiro no intervalo de 0 a 59.|  
|**MÊS (** *date_exp* **)** (ODBC 1.0)|Retorna o mês com base no campo mês de *date_exp* como um valor inteiro no intervalo de 1 a 12.|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|Retorna uma cadeia de caracteres que contém o nome específico da fonte de dados do mês (por exemplo, January a December ou Jan dezembro para uma fonte de dados que utiliza o inglês, ou Januar a Dezember para uma fonte de dados que usa alemão) para a parte do mês *date_exp*.|  
|**AGORA ()** (ODBC 1.0)|Retorna a data e hora como um valor de carimbo de hora atual.|  
|**TRIMESTRE (** *date_exp* **)** (ODBC 1.0)|Retorna o trimestre em *date_exp* como um valor inteiro no intervalo de 1 a 4, em que 1 representa 1 de janeiro a 31 de março.|  
|**SEGUNDO (** *time_exp* **)** (ODBC 1.0)|Retorna o segundo com base no campo segundo de *time_exp* como um valor inteiro no intervalo de 0 a 59.|
|**TIMESTAMPADD (** *intervalo*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|Retorna o carimbo de hora calculado adicionando *integer_exp* intervalos de tipo *intervalo* para *timestamp_exp*. Os valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> onde as frações de segundo são expressos em bilionésimos de segundo. Por exemplo, a instrução SQL a seguir retorna o nome de cada funcionário e sua data de vencimento de um ano:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Se *timestamp_exp* é um valor de tempo e *intervalo* Especifica os dias, semanas, meses, trimestres ou anos, a parte de data *timestamp_exp* é definida como a data atual antes de Calculando o carimbo de hora resultante.<br /><br /> Se *timestamp_exp* é um valor de data e *intervalo* Especifica frações segundos, segundos, minutos ou horas, a parte de hora *timestamp_exp* é definido como 0 antes de Calculando o carimbo de hora resultante.<br /><br /> Um aplicativo determina quais intervalos de uma fonte de dados oferece suporte ao chamar **SQLGetInfo** com a opção SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF (** *intervalo*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Retorna o número inteiro de intervalos de tipo *intervalo* pelo qual *timestamp_exp2* é maior do que *timestamp_exp1*. Os valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> onde as frações de segundo são expressos em bilionésimos de segundo. Por exemplo, a instrução SQL a seguir retorna o nome de cada funcionário e o número de anos, que ele foi empregado:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Se uma das expressões de carimbo de hora é um valor de hora e *intervalo* Especifica dias, semanas, meses, trimestres ou anos, a parte da data de carimbo de hora que é definida como a data atual antes de calcular a diferença entre os carimbos de hora.<br /><br /> Se uma das expressões de carimbo de hora é um valor de data e *intervalo* Especifica frações segundos, segundos, minutos ou horas, a parte de hora de carimbo de hora que é definida para 0 antes de calcular a diferença entre os carimbos de hora.<br /><br /> Um aplicativo determina quais intervalos de uma fonte de dados oferece suporte ao chamar **SQLGetInfo** com a opção SQL_TIMEDATE_DIFF_INTERVALS.|  
|**SEMANA (** *date_exp* **)** (ODBC 1.0)|Retorna a semana do ano com base no campo semana de *date_exp* como um valor inteiro no intervalo de 1 a 53.|  
|**ANO (** *date_exp* **)** (ODBC 1.0)|Retorna o ano com base no campo ano de *date_exp* como um valor inteiro. O intervalo é – dependente da fonte de dados.|
