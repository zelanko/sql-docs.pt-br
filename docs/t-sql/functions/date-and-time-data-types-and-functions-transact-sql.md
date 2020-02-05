---
title: Tipos de dados e funções de data e hora
description: Links para tipos de dados de Data e Hora e artigos de funções.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azure-sqldw-latest||= azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: a7beec472b0f4b70662c364081641b6ea91be507
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75256090"
---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>tipos de dados e funções de data e hora (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

As seções neste tópico abrangem todos os tipos e funções de data [!INCLUDE[tsql](../../includes/tsql-md.md)] e data e hora.
-   [Tipos de dados de data e hora](#DateandTimeDataTypes)  
-   [Funções de data e hora](#DateandTimeFunctions)  
    -   [Função que retorna valores de data e hora do sistema](#GetSystemDateandTimeValues)  
    -   [Funções que retornam partes de data e hora](#GetDateandTimeParts)  
    -   [Funções que retornam valores de data e hora de suas partes](#fromParts)  
    -   [Funções que retornam valores de diferença de data e hora](#GetDateandTimeDifference)  
    -   [Funções que modificam valores de data e hora](#ModifyDateandTimeValues)  
    -   [Funções que definem ou retornam funções de formato da sessão](#SetorGetSessionFormatFunctions)  
    -   [Funções que validam valores de data e hora](#ValidateDateandTimeValues)  
-   [Tópicos relacionados à data e à hora](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a> Tipos de dados de Data e Hora
Os tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)] são listados na seguinte tabela:
  
|Tipo de dados|Formatar|Intervalo|Precisão|Tamanho de armazenamento (bytes)|Precisão de segundo fracionário definida pelo usuário|Deslocamento de fuso horário|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 a 23:59:59.9999999|100 nanossegundos|3 a 5|Sim|Não|  
|[date](../../t-sql/data-types/date-transact-sql.md)|AAAA-MM-DD|0001-01-01 a 9999-12-31|1 dia|3|Não|Não|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss|01.01.00 a 06.06.79|1 minuto|4|Não|Não|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnn]|1753-01-01 a 9999-12-31|0,00333 segundo|8|Não|Não|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999|100 nanossegundos|6 a 8|Sim|Não|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999 (em UTC)|100 nanossegundos|8 a 10|Sim|Sim|  
  
> [!NOTE]  
>  O tipo de dados [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md) não é um tipo de dados de data ou hora. **timestamp** é um sinônimo preterido de **rowversion**.  
  
##  <a name="DateandTimeFunctions"></a> Funções de Data e Hora  
As tabelas a seguir listam as funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Consulte [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para obter mais informações sobre determinismo.
  
###  <a name="GetSystemDateandTimeValues"></a> Função que retorna valores de data e hora do sistema 
[!INCLUDE[tsql](../../includes/tsql-md.md)] derivam todos os valores de data e hora do sistema operacional do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada.
  
#### <a name="higher-precision-system-date-and-time-functions"></a>Funções de data e hora do sistema de precisão superior  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] deriva os valores de data e hora usando a API do Windows GetSystemTimeAsFileTime(). A precisão depende do hardware do computador e da versão do Windows no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. A API tem uma precisão fixada em 100 nanossegundos. Use a API do Windows GetSystemTimeAdjustment() para determinar a precisão.
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|Retorna um valor **datetime2(7)** que contém a data e hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada. O valor retornado não inclui o deslocamento de fuso horário.|**datetime2(7)**|Não determinístico|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|Retorna um valor **datetimeoffset(7)** que contém a data e hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada. O valor retornado inclui o deslocamento de fuso horário.|**datetimeoffset(7)**|Não determinístico|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|Retorna um valor **datetime2(7)** que contém a data e hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. A função retorna os valores de data e hora como hora UTC (Tempo Universal Coordenado).|**datetime2(7)**|Não determinístico|  
  
#### <a name="lower-precision-system-date-and-time-functions"></a>Funções de data e hora do sistema de precisão inferior
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|Retorna um valor **datetime** que contém a data e hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada. O valor retornado não inclui o deslocamento de fuso horário.|**datetime**|Não determinístico|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|Retorna um valor **datetime** que contém a data e hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada. O valor retornado não inclui o deslocamento de fuso horário.|**datetime**|Não determinístico|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|Retorna um valor **datetime** que contém a data e hora do computador no qual a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada. A função retorna os valores de data e hora como hora UTC (Tempo Universal Coordenado).|**datetime**|Não determinístico|  
  
###  <a name="GetDateandTimeParts"></a> Funções que retornam partes de data e hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *date* )|Retorna uma cadeia de caracteres que representa o *datepart* especificado da data especificada.|**nvarchar**|Não determinístico|   
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *date* )|Retorna um inteiro que representa o *datepart* especificado da *data* especificada.|**int**|Não determinístico|  
|[DAY](../../t-sql/functions/day-transact-sql.md)|DAY ( *date* )|Retorna um inteiro que representa a parte do dia da *data* especificada.|**int**|Determinística|  
|[MONTH](../../t-sql/functions/month-transact-sql.md)|MONTH ( *date* )|Retorna um inteiro que representa a parte do mês de uma *data* especificada.|**int**|Determinística|  
|[YEAR](../../t-sql/functions/year-transact-sql.md)|YEAR ( *date* )|Retorna um inteiro que representa a parte do ano de uma *data* especificada.|**int**|Determinística|  
  
###  <a name="fromParts"></a> Funções que retornam valores de data e hora de suas partes
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS  ( *year*, *month*, *day* )|Retorna um valor de **date** para o ano, o mês e o dia especificados.|**date**|Determinística|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *precision*)|Retorna um valor de **datetime2** para a data e hora especificadas, com a precisão especificada.|**datetime2(** _precision_ **)**|Determinística|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *milliseconds*)|Retorna um valor de **datetime** para a data e a hora especificadas.|**datetime**|Determinística|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *hour_offset*, *minute_offset*, *precision*)|Retorna um valor de **datetimeoffset** para a data e hora especificadas e com deslocamentos e precisão especificados.|**datetimeoffset(** _precision_ **)**|Determinística|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute* )|Retorna um valor de **smalldatetime** para a data e a hora especificadas.|**smalldatetime**|Determinística|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS  ( *hour*, *minute*, *seconds*, *fractions*, *precision* )|Retorna um valor **time** para a hora especificada, com a precisão especificada.|**time(** _precision_ **)**|Determinística|  
  
###  <a name="GetDateandTimeDifference"></a> Funções que retornam valores de diferença de data e hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|Retorna o número de limites de *datepart* de data ou hora cruzados entre duas datas especificadas.|**int**|Determinística|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|Retorna o número de limites de *datepart* de data ou hora cruzados entre duas datas especificadas.|**bigint**|Determinística|  
  
###  <a name="ModifyDateandTimeValues"></a> Funções que modificam valores de data e hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *number* , *date* )|Retorna um novo valor de **datetime** adicionando um intervalo à *datepart* especificada da *date* especificada.|O tipo de dados do argumento *date*|Determinística|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH  ( *start_date* [, *month_to_add* ] )|Retorna o último dia do mês que contém a data especificada com um deslocamento opcional.|O tipo de retorno é o tipo do argumento *start_date* ou, como alternativa, o tipo de dados **date**.|Determinística|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|SWITCHOFFSET (*DATETIMEOFFSET* , *time_zone*)|SWITCHOFFSET altera o deslocamento de fuso horário de um valor DATETIMEOFFSET e preserva o valor UTC.|**datetimeoffset** com a precisão fracionária de *DATETIMEOFFSET*|Determinística|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expression* , *time_zone*)|TODATETIMEOFFSET transforma um valor datetime2 em um valor datetimeoffset. *TODATETIMEOFFSET* interpreta o valor datetime2 no horário local, para o time_zone especificado.|**datetimeoffset** com a precisão fracionária do argumento *datetime*|Determinística|  
  
###  <a name="SetorGetSessionFormatFunctions"></a> Funções que definem ou retornam funções de formato da sessão
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|Retorna o valor atual, da sessão, de SET DATEFIRST.|**tinyint**|Não determinístico|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *number* &#124; **\@** _number_var_ }|Define o primeiro dia da semana como um número de 1 a 7.|Não aplicável|Não aplicável|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *format* &#124; **@** _format_var_ }|Define a ordem das partes de data (dia/mês/ano) para inserção de dados **datetime** ou **smalldatetime**.|Não aplicável|Não aplicável|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|Retorna o nome do idioma usado no momento. @@LANGUAGE não é uma função de data ou hora. No entanto, a definição de idioma pode afetar a saída das funções de data.|Não aplicável|Não aplicável|  
|[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE { [ N ] **'** _language_ **'** &#124; **\@** _language_var_ }|Define o ambiente de idioma para as mensagens do sistema e da sessão. SET LANGUAGE não é uma função de data ou hora. No entanto, a definição de idioma afeta a saída das funções de data.|Não aplicável|Não aplicável|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [ [ **@language =** ] **'** _language_ **'** ]|Retorna informações sobre formatos de data de todos os idiomas com suporte. **sp_helplanguage** não é um procedimento armazenado de data ou hora. No entanto, a definição de idioma afeta a saída das funções de data.|Não aplicável|Não aplicável|  
  
###  <a name="ValidateDateandTimeValues"></a> Funções que validam valores de data e hora
  
|Função|Sintaxe|Valor retornado|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *expression* )|Determina se uma expressão de entrada **datetime** ou **smalldatetime** tem um valor de data ou hora válido.|**int**|ISDATE só será determinística se usada com a função CONVERT, quando o parâmetro de estilo CONVERT for especificado e o estilo não for igual a 0, 100, 9 nem 109.|  
  
##  <a name="DateandTimeRelatedTopics"></a> Tópicos relacionados à data e à hora 
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|Fornece informações sobre a conversão de valores de data e hora para e de literais de cadeia de caracteres, bem como outros formatos de data e hora.|  
|[Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)|Fornece diretrizes para a portabilidade de bancos de dados e aplicativos de bancos de dados que usam instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de um idioma a outro, ou que dão suporte a vários idiomas.|  
|[Funções escalares ODBC &#40;Transact-SQL&#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|Fornece informações sobre as funções escalares ODBC disponíveis para uso em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Isso inclui funções de data e hora ODBC.|  
|[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|Fornece conversão de fuso horário.|  
  
## <a name="see-also"></a>Confira também
[Funções](../../t-sql/functions/functions.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
