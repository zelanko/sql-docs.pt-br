---
title: "Dados de data e hora tipos e funções (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 7ce3baac7ec87ff3cad771234ab1196fb0a3855e
ms.contentlocale: pt-br
ms.lasthandoff: 09/06/2017

---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>tipos de dados e funções de data e hora (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

As seções a seguir neste tópico fornecem uma visão geral de todos os tipos de dados e funções de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)].
-   [Tipos de dados de hora e data](#DateandTimeDataTypes)  
-   [Funções de data e hora](#DateandTimeFunctions)  
    -   [Função que valores Get sistema data e hora](#GetSystemDateandTimeValues)  
    -   [Funções que obtêm a data e hora partes](#GetDateandTimeParts)  
    -   [Funções que obtêm valores de data e hora de suas partes](#fromParts)  
    -   [Funções que obtêm a data e hora de diferença](#GetDateandTimeDifference)  
    -   [Funções que modificam a data e valores de tempo](#ModifyDateandTimeValues)  
    -   [Funções que definem ou obtêm funções de formato de sessão](#SetorGetSessionFormatFunctions)  
    -   [Funções que validam a data e valores de tempo](#ValidateDateandTimeValues)  
-   [Data e tópicos relacionados a tempo](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a>Tipos de dados de data e hora
O [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora são listados na tabela a seguir:
  
|Tipo de dados|Formato|Intervalo|Precisão|Tamanho de armazenamento (bytes)|Precisão de segundo fracionário definida pelo usuário|Deslocamento de fuso horário|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 a 23:59:59.9999999|100 nanossegundos|3 a 5|Sim|Não|  
|[date](../../t-sql/data-types/date-transact-sql.md)|AAAA-MM-DD|0001-01-01 a 9999-12-31|1 dia|3|Não|Não|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss|01.01.00 a 06.06.79|1 minuto|4|Não|Não|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnn]|1753-01-01 a 9999-12-31|0,00333 segundo|8|Não|Não|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999|100 nanossegundos|6 a 8|Sim|Não|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|AAAA-MM-DD HH [. nnnnnnn] [+ &#124;-] hh: mm|0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999 (em UTC)|100 nanossegundos|8 a 10|Sim|Sim|  
  
> [!NOTE]  
>  O [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md) tipo de dados não é um tipo de dados de data ou hora. **carimbo de hora** é um sinônimo preterido para **rowversion**.  
  
##  <a name="DateandTimeFunctions"></a>Funções de data e hora  
As funções de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)] são apresentadas nas tabelas a seguir. Para obter mais informações sobre determinismo, consulte [determinísticas e funções não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
###  <a name="GetSystemDateandTimeValues"></a>Funções que obtêm valores de data e hora de sistema 
Todos os valores de data e hora do sistema são derivados do sistema operacional do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.
  
#### <a name="higher-precision-system-date-and-time-functions"></a>Funções de data e hora do sistema de precisão superior  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Obtém os valores de data e hora usando a API do Windows GetSystemTimeAsFileTime(). A precisão depende do hardware do computador e da versão do Windows no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. A precisão desta API está fixada em 100 nanosegundos. A precisão pode ser determinada usando a API do Windows GetSystemTimeAdjustment().
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|Retorna um **datetime2 (7)** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. O deslocamento de fuso horário não está incluído.|**datetime2(7)**|Não determinístico|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|Retorna um **datetimeoffset(7)** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. O deslocamento de fuso horário está incluído.|**DateTimeOffset(7)**|Não determinístico|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|Retorna um **datetime2 (7)** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. A data e hora é retornada como hora UTC (Coordinated Universal Time).|**datetime2(7)**|Não determinístico|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>Funções de data e hora do sistema de precisão inferior
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|Retorna um **datetime** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. O deslocamento de fuso horário não está incluído.|**datetime**|Não determinístico|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|Retorna um **datetime** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. O deslocamento de fuso horário não está incluído.|**datetime**|Não determinístico|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|Retorna um **datetime** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. A data e hora é retornada como hora UTC (Coordinated Universal Time).|**datetime**|Não determinístico|  
  
###  <a name="GetDateandTimeParts"></a>Funções que obtêm partes de data e hora
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *data* )|Retorna uma cadeia de caracteres que representa a *datepart* da data especificada.|**nvarchar**|Não determinístico|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *data* )|Retorna um inteiro que representa a *datepart* especificada *data*.|**int**|Não determinístico|  
|[DIA](../../t-sql/functions/day-transact-sql.md)|DIA ( *data* )|Retorna um inteiro que representa a parte do dia especificada *data*.|**int**|Determinística|  
|[MÊS](../../t-sql/functions/month-transact-sql.md)|MÊS ( *data* )|Retorna um inteiro que representa a parte do mês de um especificado *data*.|**int**|Determinística|  
|[ANO](../../t-sql/functions/year-transact-sql.md)|ANO ( *data* )|Retorna um inteiro que representa a parte do ano de determinado *data*.|**int**|Determinística|  
  
###  <a name="fromParts"></a>Funções que obtêm valores de data e hora de suas partes
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS ( *ano*, *mês*, *dia* )|Retorna um **data** valor para o ano especificado, mês e dia.|**date**|Determinística|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS ( *ano*, *mês*, *dia*, *hora*, *minuto*, *segundos* , *frações*, *precisão*)|Retorna um **datetime2** valor para a data e hora especificadas e com a precisão especificada.|**datetime2 (** *precisão* **)**|Determinística|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS ( *ano*, *mês*, *dia*, *hora*, *minuto*, *segundos* , *milissegundos*)|Retorna um **datetime** valor para a data e hora especificadas.|**datetime**|Determinística|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS ( *ano*, *mês*, *dia*, *hora*, *minuto*,  *segundos*, *frações*, *hour_offset*, *minute_offset*, *precisão*)|Retorna um **datetimeoffset** valor para a data e hora especificadas e com os deslocamentos e precisão especificados.|**Data e hora (** *precisão* **)**|Determinística|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS ( *ano*, *mês*, *dia*, *hora*, *minuto* )|Retorna um **smalldatetime** valor para a data e hora especificadas.|**smalldatetime**|Determinística|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS ( *hora*, *minuto*, *segundos*, *frações*, *precisão* )|Retorna um **tempo** valor para o tempo especificado e com a precisão especificada.|**tempo (** *precisão* **)**|Determinística|  
  
###  <a name="GetDateandTimeDifference"></a>Funções que obtêm diferença de data e hora
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|Retorna o número de data ou hora *datepart* limites que são cruzados entre duas datas especificadas.|**int**|Determinística|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|Retorna o número de data ou hora *datepart* limites que são cruzados entre duas datas especificadas.|**bigint**|Determinística|  
  
###  <a name="ModifyDateandTimeValues"></a>Funções que modificam os valores de data e hora
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *número* , *data* )|Retorna um novo **datetime** valor adicionando um intervalo especificado *datepart* especificada *data*.|O tipo de dados de *data* argumento|Determinística|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH ( *start_date* [, *month_to_add* ])|Retorna o último dia do mês que contém a data especificada com um deslocamento opcional.|Tipo de retorno é o tipo de *start_date* ou **data**.|Determinística|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|OPÇÃO*deslocamento* (*DATETIMEOFFSET* , *fuso_horário*)|OPÇÃO*deslocamento* altera o deslocamento de fuso horário do valor DATETIMEOFFSET e preserva o valor UTC.|**DateTimeOffset** com a precisão fracionária de *DATETIMEOFFSET*|Determinística|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expressão* , *fuso_horário*)|TODATETIMEOFFSET transforma um valor datetime2 em um valor datetimeoffset. O valor datetime2 é interpretado em hora local para time_zone especificado.|**DateTimeOffset** com a precisão fracionária de *datetime* argumento|Determinística|  
  
###  <a name="SetorGetSessionFormatFunctions"></a>Funções que obtém ou defina o formato de sessão
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|Retorna o valor atual, da sessão, de SET DATEFIRST.|**tinyint**|Não determinístico|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *número* &#124;  **@**  *number_var* }|Define o primeiro dia da semana como um número de 1 a 7.|Não aplicável|Não aplicável|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *formato* &#124;  **@**  *format_var* }|Define a ordem das partes de data (dia/mês/ano) para inserir **datetime** ou **smalldatetime** dados.|Não aplicável|Não aplicável|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|Retorna o nome do idioma que está sendo usado. @@LANGUAGE não é uma função de data ou hora. No entanto, a definição de idioma pode afetar a saída das funções de data.|Não aplicável|Não aplicável|  
|[CONJUNTO DE LINGUAGEM](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE {[N] **'***idioma***'** &#124;  **@**  *language_var* }|Define o ambiente de idioma para as mensagens do sistema e da sessão. SET LANGUAGE não é uma função de data ou hora. No entanto, a definição de idioma afeta a saída das funções de data.|Não aplicável|Não aplicável|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [[  **@language =** ] **'***idioma***'** ]|Retorna informações sobre formatos de data de todos os idiomas com suporte. **sp_helplanguage** não é uma data ou hora procedimento armazenado. No entanto, a definição de idioma afeta a saída das funções de data.|Não aplicável|Não aplicável|  
  
###  <a name="ValidateDateandTimeValues"></a>Funções que validam valores de data e hora
  
|Função|Sintaxe|Valor de retorno|Tipo de dados de retorno|Determinismo|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *expressão* )|Determina se um **datetime** ou **smalldatetime** expressão de entrada é uma data válida ou um valor de tempo.|**int**|ISDATE só será determinística se você usá-la com a função CONVERT, quando o parâmetro de estilo CONVERT for especificado e o estilo não for igual a 0, 100, 9 nem 109.|  
  
##  <a name="DateandTimeRelatedTopics"></a>Data e tópicos relacionados a tempo 
  
|Tópico|Description|  
|-----------|-----------------|  
|[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|Fornece informações sobre a conversão de valores de data e hora para e de literais de cadeia de caracteres, bem como outros formatos de data e hora.|  
|[Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)|Fornece diretrizes para a portabilidade de bancos de dados e aplicativos de banco de dados que usam [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções de um idioma para outro, ou que oferecem suporte a vários idiomas.|  
|[Funções escalares ODBC &#40; Transact-SQL &#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|Fornece informações sobre funções escalares ODBC que podem ser usados em [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções. Isso inclui funções de data e hora do ODBC.|  
|[FUSO horário &AMP; #40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|Fornece conversão de fuso horário.|  
  
## <a name="see-also"></a>Consulte também
[Funções](../../t-sql/functions/functions.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

