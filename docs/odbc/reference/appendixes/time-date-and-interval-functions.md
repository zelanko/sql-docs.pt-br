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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aec3d6b23383edcc9659ff884e8cd71b0595dae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302817"
---
# <a name="time-date-and-interval-functions"></a>Funções de hora, data e intervalo
A tabela a seguir lista as funções de hora e data incluídas no conjunto de funções escalares ODBC. Um aplicativo pode determinar quais funções de hora e data são suportadas por um driver ligando para **o SQLGetInfo** com um tipo de SQL_TIMEDATE_FUNCTIONS de *informações.*  
  
 Os argumentos denotados como *timestamp_exp* podem ser o nome de uma coluna, o resultado de outra função escalar, ou uma *fuga de tempo oDBC,* *fuga de data-Data ODBC*ou *fuga de carimbo de tempo oDBC,* onde o tipo de dados subjacente poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotados como *date_exp* podem ser o nome de uma coluna, o resultado de outra função escalar, ou uma *fuga de data oDBC* ou *fuga de carimbo de data ODBC,* onde o tipo de dados subjacente poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE ou SQL_TYPE_TIMESTAMP.  
  
 Argumentos denotados como *time_exp* podem ser o nome de uma coluna, o resultado de outra função escalar, ou uma *fuga de tempo oDBC* ou *fuga de carimbo de tempo oDBC,* onde o tipo de dados subjacente poderia ser representado como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP.  
  
 As funções escalares CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP foram adicionadas no ODBC 3.0 para se alinharem ao SQL-92.  
  
|Função|Descrição|  
|--------------|-----------------|  
|**CURRENT_DATE(** ODBC 3.0)|Retorna a data atual.|  
|**CURRENT_TIME[(time-precision)]** *time-precision* **)]** (ODBC 3.0)|Retorna a hora local atual. O *argumento de precisão de tempo* determina a precisão dos segundos do valor devolvido.|  
|**CURRENT_TIMESTAMP**<br /> *[((timestamp-precision)]* **)]** (ODBC 3.0) **[(**|Retorna a data local atual e a hora local como um valor de carimbo de data e hora. O argumento *de precisão de carimbo de tempo* determina a precisão dos segundos do carimbo de tempo devolvido.|  
|**CURDATE** (ODBC 1.0)|Retorna a data atual.|  
|**CURTIME()** (ODBC 1.0)|Retorna a hora local atual.|  
|**DAYNAME** *(date_exp)* **)** (ODBC 2.0)|Retorna uma seqüência de caracteres contendo o nome específico da fonte de dados do dia (por exemplo, de domingo a sábado ou domingo ou sol. a Sat. para uma fonte de dados que usa inglês, ou Sonntag através do Samstag para uma fonte de dados que usa alemão) para a parte do dia de *date_exp*.|  
|**DAYOFMONTH** *(date_exp)* **)** (ODBC 1.0)|Retorna o dia do mês com base no campo do mês em *date_exp* como um valor inteiro na faixa de 1-31.|  
|**DAYOFWEEK** *(date_exp)* **)** (ODBC 1.0)|Retorna o dia da semana com base no campo da semana em *date_exp* como um valor inteiro na faixa de 1-7, onde 1 representa domingo.|  
|**DAYOFYEAR** *(date_exp)* **)** (ODBC 1.0)|Retorna o dia do ano com base no campo do ano em *date_exp* como um valor inteiro na faixa de 1-366.|  
|**EXTRACT** *(extrato-campo da* *fonte de extrato)* **)** (ODBC 3.0)|Retorna a parte do *campo de extração* da *fonte de extrato*. O argumento *da fonte de extrato* é uma expressão de data ou intervalo. O argumento *extrato-campo* pode ser uma das seguintes palavras-chave:<br /><br /> MÊS DO MÊS MINUTO HORA SEGUNDO<br /><br /> A precisão do valor devolvido é definida pela implementação. A escala é de 0 a menos que o SEGUNDO seja especificado, nesse caso a escala não é menor que a precisão de segundos fracionados do campo *de origem do extrato.*|  
|**HORA(** *time_exp* **)** (ODBC 1.0)|Retorna a hora com base no campo de horas em *time_exp* como um valor inteiro na faixa de 0-23.|  
|**MINUTO(** *time_exp* **)** (ODBC 1.0)|Retorna o minuto baseado no campo de *minutos* em time_exp como um valor inteiro na faixa de 0-59.|  
|**MÊS** *(date_exp)* **)** (ODBC 1.0)|Retorna o mês com base no campo do mês em *date_exp* como um valor inteiro na faixa de 1-12.|  
|**MONTHNAME(** *MONTHNAME (date_exp)* **)** (ODBC 2.0)|Retorna uma seqüência de caracteres contendo o nome específico de origem de dados do mês (por exemplo, janeiro a dezembro ou janeiro até dezembro para uma fonte de dados que usa inglês, ou Januar através de Dezember para uma fonte de dados que usa alemão) para a parte do mês de *date_exp*.|  
|**NOW ()** (ODBC 1.0)|Retorna a data e a hora atuais como um valor de carimbo de data-hora.|  
|**QUARTER(** *(date_exp)* **)** (ODBC 1.0)|Retorna o trimestre em *date_exp* como um valor inteiro na faixa de 1-4, onde 1 representa 1 de janeiro a 31 de março.|  
|**SEGUNDO (** *time_exp* **)** (ODBC 1.0)|Retorna o segundo com base no segundo campo em *time_exp* como um valor inteiro na faixa de 0-59.|
|**TIMESTAMPADD** *(intervalo,* *integer_exp*, *timestamp_exp)* **)** (ODBC 2.0)|Retorna o carimbo de tempo calculado adicionando *intervalos* de integer_exp do intervalo de *tipo* para *timestamp_exp*. Valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> onde segundos fracionados são expressos em bilionésimos de segundo. Por exemplo, a seguinte declaração SQL retorna o nome de cada funcionário e sua data de aniversário de um ano:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Se *timestamp_exp* for um valor de tempo e *intervalo* especificar dias, semanas, meses, trimestres ou anos, a parte da data de *timestamp_exp* é definida para a data atual antes de calcular o carimbo de tempo resultante.<br /><br /> Se *timestamp_exp* for um valor de data e *intervalo* especificar segundos fracionários, segundos, minutos ou horas, a parte de tempo do *timestamp_exp* é definida como 0 antes de calcular o carimbo de tempo resultante.<br /><br /> Um aplicativo determina quais intervalos uma fonte de dados suporta ligando para **o SQLGetInfo** com a opção SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF** *(intervalo*, *timestamp_exp1*, *timestamp_exp2)* **)** (ODBC 2.0)|Retorna o número inteiro de intervalos de *tipo* pelos *quais timestamp_exp2* é maior do que *timestamp_exp1*. Valores válidos de *intervalo* são as seguintes palavras-chave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> onde segundos fracionados são expressos em bilionésimos de segundo. Por exemplo, a seguinte declaração SQL retorna o nome de cada funcionário e o número de anos que ele ou ela foi empregado:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Se qualquer expressão de carimbo de tempo for um valor de tempo e *intervalo* especificar dias, semanas, meses, trimestres ou anos, a parte da data desse carimbo de tempo é definida para a data atual antes de calcular a diferença entre os carimbos de tempo.<br /><br /> Se a expressão do carimbo de data for um valor de data e *o intervalo* especificar segundos fracionários, segundos, minutos ou horas, a parte de tempo desse carimbo de tempo será definida como 0 antes de calcular a diferença entre os carimbos de tempo.<br /><br /> Um aplicativo determina quais intervalos uma fonte de dados suporta ligando para **o SQLGetInfo** com a opção SQL_TIMEDATE_DIFF_INTERVALS.|  
|**SEMANA** *(date_exp)* **)** (ODBC 1.0)|Retorna a semana do ano com base no campo da semana em *date_exp* como um valor inteiro na faixa de 1-53.|  
|**YEAR(** *(date_exp)* **)** (ODBC 1.0)|Retorna o ano com base no campo de ano em *date_exp* como um valor inteiro. O intervalo é dependente da fonte de dados.|
