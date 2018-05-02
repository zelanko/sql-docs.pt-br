---
title: Tipos de dados e funções de data e hora (Transact-SQL)| Microsoft Docs
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
caps.latest.revision: 79
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7dae37763b4a4ef372964ad3990fa77adaae1f0d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>tipos de dados e funções de data e hora (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

As seções a seguir neste tópico fornecem uma visão geral de todos os tipos de dados e funções de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)].
-   [Tipos de dados de data e hora](#DateandTimeDataTypes)  
-   [Funções de data e hora](#DateandTimeFunctions)  
    -   [Função que obtém valores de data e hora do sistema](#GetSystemDateandTimeValues)  
    -   [Funções que obtêm partes de data e hora](#GetDateandTimeParts)  
    -   [Funções que obtêm valores de data e hora de suas partes](#fromParts)  
    -   [Funções que obtêm a diferença de data e hora](#GetDateandTimeDifference)  
    -   [Funções que modificam valores de data e hora](#ModifyDateandTimeValues)  
    -   [Funções que definem ou obtêm funções de formato da sessão](#SetorGetSessionFormatFunctions)  
    -   [Funções que validam valores de data e hora](#ValidateDateandTimeValues)  
-   [Tópicos relacionados à data e à hora](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a> Tipos de dados de Data e Hora
Os tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)] são listados na seguinte tabela:
  
|Tipo de dados|Formato|Intervalo|Precisão|Tamanho de armazenamento (bytes)|Precisão de segundo fracionário definida pelo usuário|Deslocamento de fuso horário|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 a 23:59:59.9999999|100 nanossegundos|3 a 5|Sim|não|  
|[date](../../t-sql/data-types/date-transact-sql.md)|AAAA-MM-DD|0001-01-01 a 9999-12-31|1 dia|3|não|não|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss|01.01.00 a 06.06.79|1 minuto|4|não|não|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnn]|1753-01-01 a 9999-12-31|0,00333 segundo|8|não|não|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999|100 nanossegundos|6 a 8|Sim|não|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999 (em UTC)|100 nanossegundos|8 a 10|Sim|Sim|  
  
> [!NOTE]  
>  O tipo de dados [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md) não é um tipo de dados de data ou hora. **timestamp** é um sinônimo preterido de **rowversion**.  
  
##  <a name="DateandTimeFunctions"></a> Funções de Data e Hora  
As funções de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)] são apresentadas nas tabelas a seguir. Para obter mais informações sobre determinismo de funções, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
###  <a name="GetSystemDateandTimeValues"></a> Funções que obtêm valores de Data e Hora do sistema 
Todos os valores de data e hora do sistema são derivados do sistema operacional do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.
  
#### <a name="higher-precision-system-date-and-time-functions"></a>Funções de data e hora do sistema de precisão superior  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] obtém os valores de data e hora usando a API do Windows GetSystemTimeAsFileTime(). A precisão depende do hardware do computador e da versão do Windows no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. A precisão desta API está fixada em 100 nanosegundos. A precisão pode ser determinada usando a API do Windows GetSystemTimeAdjustment().
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|Retorna um valor de **datetime2(7)** que contém a data e a hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. O deslocamento de fuso horário não está incluído.|**datetime2(7)**|Não determinístico|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|Retorna um valor de **datetimeoffset(7)** que contém a data e a hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. O deslocamento de fuso horário está incluído.|**datetimeoffset(7)**|Não determinístico|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|Retorna um valor de **datetime2(7)** que contém a data e a hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. A data e hora são retornadas como hora UTC (Tempo Universal Coordenado).|**datetime2(7)**|Não determinístico|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>Funções de data e hora do sistema de precisão inferior
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|Retorna um valor de **datetime** que contém a data e a hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. O deslocamento de fuso horário não está incluído.|**datetime**|Não determinístico|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|Retorna um valor de **datetime** que contém a data e a hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. O deslocamento de fuso horário não está incluído.|**datetime**|Não determinístico|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|Retorna um valor de **datetime** que contém a data e a hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. A data e hora são retornadas como hora UTC (Tempo Universal Coordenado).|**datetime**|Não determinístico|  
  
###  <a name="GetDateandTimeParts"></a> Funções que obtêm partes de Data e Hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *date* )|Retorna uma cadeia de caracteres que representa a *datepart* especificada da data especificada.|**nvarchar**|Não determinístico|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *date* )|Retorna um inteiro que representa a *datepart* especificada da *date* informada.|**int**|Não determinístico|  
|[DAY](../../t-sql/functions/day-transact-sql.md)|DAY ( *date* )|Retorna um inteiro que representa a parte do dia da *date* especificada.|**int**|Determinística|  
|[MONTH](../../t-sql/functions/month-transact-sql.md)|MONTH ( *date* )|Retorna um inteiro que representa a parte do mês de uma *date* especificada.|**int**|Determinística|  
|[YEAR](../../t-sql/functions/year-transact-sql.md)|YEAR ( *date* )|Retorna um inteiro que representa a parte do ano de uma *date* especificada.|**int**|Determinística|  
  
###  <a name="fromParts"></a> Funções que obtêm valores de Data e Hora de suas partes
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS  ( *year*, *month*, *day* )|Retorna um valor de **date** para o ano, o mês e o dia especificados.|**date**|Determinística|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *precision*)|Retorna um valor de **datetime2** para a data e hora especificadas e com a precisão especificada.|**datetime2(** *precision* **)**|Determinística|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *milliseconds*)|Retorna um valor de **datetime** para a data e a hora especificadas.|**datetime**|Determinística|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *hour_offset*, *minute_offset*, *precision*)|Retorna um valor de **datetimeoffset** para a data e hora especificadas e com deslocamentos e precisão especificados.|**datetimeoffset(** *precision* **)**|Determinística|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute* )|Retorna um valor de **smalldatetime** para a data e a hora especificadas.|**smalldatetime**|Determinística|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS  ( *hour*, *minute*, *seconds*, *fractions*, *precision* )|Retorna um valor **time** para a hora especificada e com a precisão especificada.|**time(** *precision* **)**|Determinística|  
  
###  <a name="GetDateandTimeDifference"></a> Funções que obtêm a diferença de Data e Hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|Retorna o número de limites de *datepart* de data ou hora entre duas datas especificadas.|**int**|Determinística|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|Retorna o número de limites de *datepart* de data ou hora entre duas datas especificadas.|**bigint**|Determinística|  
  
###  <a name="ModifyDateandTimeValues"></a> Funções que modificam valores de Data e Hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *number* , *date* )|Retorna um novo valor de **datetime** adicionando um intervalo à *datepart* especificada da *date* especificada.|O tipo de dados do argumento *date*|Determinística|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH  ( *start_date* [, *month_to_add* ] )|Retorna o último dia do mês que contém a data especificada com um deslocamento opcional.|O tipo de retorno é o tipo de *start_date* ou **date**.|Determinística|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|SWITCH*OFFSET* (*DATETIMEOFFSET* , *time_zone*)|SWITCH*OFFSET* altera o deslocamento de fuso horário de um valor DATETIMEOFFSET e preserva o valor UTC.|**datetimeoffset** com a precisão fracionária de *DATETIMEOFFSET*|Determinística|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expression* , *time_zone*)|TODATETIMEOFFSET transforma um valor datetime2 em um valor datetimeoffset. O valor datetime2 é interpretado em hora local para time_zone especificado.|**datetimeoffset** com a precisão fracionária do argumento *datetime*|Determinística|  
  
###  <a name="SetorGetSessionFormatFunctions"></a> Funções que obtêm ou definem o formato da sessão
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|Retorna o valor atual, da sessão, de SET DATEFIRST.|**tinyint**|Não determinístico|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *number* &#124; **@***number_var* }|Define o primeiro dia da semana como um número de 1 a 7.|Não aplicável|Não aplicável|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *format* &#124; **@***format_var* }|Define a ordem das partes de data (dia/mês/ano) para inserção de dados **datetime** ou **smalldatetime**.|Não aplicável|Não aplicável|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|Retorna o nome do idioma que está sendo usado atualmente. @@LANGUAGE não é uma função de data ou hora. No entanto, a definição de idioma pode afetar a saída das funções de data.|Não aplicável|Não aplicável|  
|[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE { [ N ] **'***language***'** &#124; **@***language_var* }|Define o ambiente de idioma para as mensagens do sistema e da sessão. SET LANGUAGE não é uma função de data ou hora. No entanto, a definição de idioma afeta a saída das funções de data.|Não aplicável|Não aplicável|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [ [ **@language =** ] **'***language***'** ]|Retorna informações sobre formatos de data de todos os idiomas com suporte. **sp_helplanguage** não é um procedimento armazenado de data ou hora. No entanto, a definição de idioma afeta a saída das funções de data.|Não aplicável|Não aplicável|  
  
###  <a name="ValidateDateandTimeValues"></a> Funções que validam valores de Data e Hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *expression* )|Determina se uma expressão de entrada **datetime** ou **smalldatetime** é um valor de data ou hora válido.|**int**|ISDATE só será determinística se você usá-la com a função CONVERT, quando o parâmetro de estilo CONVERT for especificado e o estilo não for igual a 0, 100, 9 nem 109.|  
  
##  <a name="DateandTimeRelatedTopics"></a> Tópicos relacionados à data e à hora 
  
|Tópico|Description|  
|-----------|-----------------|  
|[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|Fornece informações sobre a conversão de valores de data e hora para e de literais de cadeia de caracteres, bem como outros formatos de data e hora.|  
|[Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)|Fornece diretrizes para a portabilidade de bancos de dados e aplicativos de bancos de dados que usam instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de um idioma a outro, ou que dão suporte a vários idiomas.|  
|[Funções escalares ODBC &#40;Transact-SQL&#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|Fornece informações sobre as funções escalares ODBC que podem ser usadas em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Isso inclui funções de data e hora ODBC.|  
|[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|Fornece conversão de fuso horário.|  
  
## <a name="see-also"></a>Confira também
[Funções](../../t-sql/functions/functions.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
