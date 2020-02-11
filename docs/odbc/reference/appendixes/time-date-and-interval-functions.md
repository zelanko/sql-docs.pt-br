---
title: Funções de hora, data e intervalo | Microsoft Docs
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
ms.openlocfilehash: ae10946be501adb16fdda5fa9f053e389eea4bed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070079"
---
# <a name="time-date-and-interval-functions"></a>Funções de hora, data e intervalo
A tabela a seguir lista as funções de data e hora incluídas no conjunto de funções escalares ODBC. Um aplicativo pode determinar quais funções de data e hora têm suporte por um driver chamando **SQLGetInfo** com um *tipo de informação* de SQL_TIMEDATE_FUNCTIONS.  
  
 Argumentos denotados como *timestamp_exp* podem ser o nome de uma coluna, o resultado de outra função escalar ou um ODBC- *time-* escape, *ODBC-Date-escape*ou *ODBC-timestamp-escape*, em que o tipo de dados subjacente poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos indicados como *date_exp* podem ser o nome de uma coluna, o resultado de outra função escalar ou um *ODBC-Data-escape* ou *ODBC-timestamp-escape*, em que o tipo de dados subjacente poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos indicados como *time_exp* podem ser o nome de uma coluna, o resultado de outra função escalar ou um ODBC- *time-* escape ou *ODBC-timestamp-escapar*, em que o tipo de dados subjacente poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP.  
  
 Os CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP funções escalares de data e momento foram adicionados no ODBC 3,0 para serem alinhados com o SQL-92.  
  
|Função|DESCRIÇÃO|  
|--------------|-----------------|  
|**CURRENT_DATE ()** (ODBC 3,0)|Retorna a data atual.|  
|**CURRENT_TIME [(** *precisão de tempo* **)]** (ODBC 3,0)|Retorna a hora local atual. O argumento de *precisão de tempo* determina a precisão de segundos do valor retornado.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *carimbo de data/hora-precisão* **)]** (ODBC 3,0)|Retorna a data local atual e a hora local como um valor timestamp. O argumento *de precisão de carimbo de data/hora* determina a precisão de segundos do carimbo de data/hora retornado.|  
|**CURDATE ()** (ODBC 1,0)|Retorna a data atual.|  
|**CURTIME ()** (ODBC 1,0)|Retorna a hora local atual.|  
|**DAYNAME (** *date_exp* **)** (ODBC 2,0)|Retorna uma cadeia de caracteres que contém o nome específico da fonte de dados do dia (por exemplo, domingo a sábado ou sol. a Sat. para uma fonte de dados que usa o inglês ou Sonntag por meio de Samstag para uma fonte de dados que usa alemão) para a parte do dia de *date_exp*.|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1,0)|Retorna o dia do mês com base no campo mês em *date_exp* como um valor inteiro no intervalo de 1-31.|  
|**DayOfWeek (** *date_exp* **)** (ODBC 1,0)|Retorna o dia da semana com base no campo semana em *date_exp* como um valor inteiro no intervalo de 1-7, em que 1 representa domingo.|  
|**DayOfYear (** *date_exp* **)** (ODBC 1,0)|Retorna o dia do ano com base no campo year em *date_exp* como um valor inteiro no intervalo de 1-366.|  
|**Extrair (** *extrair-Field de* *extrair-Source* **)** (ODBC 3,0)|Retorna a parte do *campo de extração* da *fonte de extração*. O argumento *de fonte de extração* é uma expressão DateTime ou Interval. O argumento *Extract-Field* pode ser uma das seguintes palavras-chave:<br /><br /> ANO MÊS DIA HORA SEGUNDO MINUTO<br /><br /> A precisão do valor retornado é definida pela implementação. A escala é 0 a menos que a segunda seja especificada; nesse caso, a escala não é menor que a precisão de segundos fracionários do campo de *fonte de extração* .|  
|**Hora (** *time_exp* **)** (ODBC 1,0)|Retorna a hora com base no campo de hora em *time_exp* como um valor inteiro no intervalo de 0-23.|  
|**Minuto (** *time_exp* **)** (ODBC 1,0)|Retorna o minuto com base no campo de minuto em *time_exp* como um valor inteiro no intervalo de 0-59.|  
|**Mês (** *date_exp* **)** (ODBC 1,0)|Retorna o mês com base no campo mês em *date_exp* como um valor inteiro no intervalo de 1-12.|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2,0)|Retorna uma cadeia de caracteres que contém o nome específico da fonte de dados do mês (por exemplo, janeiro a Dezembro ou Jan. até Dec. para uma fonte de dados que usa o inglês ou januar por meio de Dezember para uma fonte de dados que usa alemão) para a parte do mês de *date_exp*.|  
|**Now ()** (ODBC 1,0)|Retorna a data e a hora atuais como um valor timestamp.|  
|**Trimestre (** *date_exp* **)** (ODBC 1,0)|Retorna o trimestre em *date_exp* como um valor inteiro no intervalo de 1-4, em que 1 representa 1º de janeiro a 31 de março.|  
|**Segundo (** *time_exp* **)** (ODBC 1,0)|Retorna o segundo com base no segundo campo em *time_exp* como um valor inteiro no intervalo de 0-59.|
|**TIMESTAMPADD (** *intervalo*, *integer_exp*, *timestamp_exp* **)** (ODBC 2,0)|Retorna o carimbo de data/hora calculado adicionando *integer_exp* intervalos do tipo *intervalo* a *timestamp_exp*. Os valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> em que os segundos fracionários são expressos em billionths de um segundo. Por exemplo, a seguinte instrução SQL retorna o nome de cada funcionário e sua data de aniversário de um ano:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Se *timestamp_exp* for um valor de tempo e um *intervalo* especificar dias, semanas, meses, trimestres ou anos, a parte de data de *timestamp_exp* será definida como a data atual antes de calcular o carimbo de data/hora resultante.<br /><br /> Se *timestamp_exp* for um valor de data e um *intervalo* especificar segundos fracionários, segundos, minutos ou horas, a parte de tempo de *timestamp_exp* será definida como 0 antes de calcular o carimbo de data/hora resultante.<br /><br /> Um aplicativo determina quais intervalos uma fonte de dados dá suporte chamando **SQLGetInfo** com a opção SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF (** *intervalo*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2,0)|Retorna o número inteiro de intervalos do tipo *intervalo* pelo qual *timestamp_exp2* é maior que *timestamp_exp1*. Os valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> em que os segundos fracionários são expressos em billionths de um segundo. Por exemplo, a seguinte instrução SQL retorna o nome de cada funcionário e o número de anos que ele tem sido empregado:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Se a expressão de carimbo de data/hora for um valor de tempo e um *intervalo* especificar dias, semanas, meses, trimestres ou anos, a parte de data desse carimbo de hora será definida como a data atual antes de calcular a diferença entre os carimbos de hora.<br /><br /> Se uma das expressões timestamp for um valor de data e um *intervalo* especificar segundos fracionários, segundos, minutos ou horas, a parte de tempo desse carimbo de data/hora será definida como 0 antes de calcular a diferença entre os carimbos de hora.<br /><br /> Um aplicativo determina quais intervalos uma fonte de dados dá suporte chamando **SQLGetInfo** com a opção SQL_TIMEDATE_DIFF_INTERVALS.|  
|**Semana (** *date_exp* **)** (ODBC 1,0)|Retorna a semana do ano com base no campo semana em *date_exp* como um valor inteiro no intervalo de 1-53.|  
|**Year (** *date_exp* **)** (ODBC 1,0)|Retorna o ano com base no campo year em *date_exp* como um valor inteiro. O intervalo é dependente da fonte de dados.|
