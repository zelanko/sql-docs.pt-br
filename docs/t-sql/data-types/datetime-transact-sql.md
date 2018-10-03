---
title: datetime (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- datetime_TSQL
- datetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetime
- dates [SQL Server], data types
- datetime data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: 9bd1cc5b-227b-4032-95d6-7581ddcc9924
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3e83229dde185bb4744e89fabbf88ddf3cabaa3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720384"
---
# <a name="datetime-transact-sql"></a>datetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define uma data combinada com uma hora do dia que inclui frações de segundos e se baseia em um período de 24 horas.
  
> [!NOTE]  
>  Use os tipos de dados **time**, **date**, **datetime2** e **datetimeoffset** para o novo trabalho. Esses tipos estão de acordo com o SQL padrão. Eles são mais portáteis. **time**, **datetime2** e **datetimeoffset** fornecem mais precisão de segundos. **datetimeoffset** é compatível com fuso horário para aplicativos implantados globalmente.  
  
## <a name="datetime-description"></a>Descrição de datetime  
  
|Propriedade|Valor|  
|---|---|
|Sintaxe|**datetime**|  
|Uso|DECLARE \@MyDatetime **datetime**<br /><br /> CREATE TABLE Table1 ( Column1 **datetime** )|  
|Formatos de literais de cadeia de caracteres padrão<br /><br /> (usado para cliente de nível inferior)|Não aplicável|  
|Intervalo de datas|Janeiro 1, 1753, a dezembro 31, 9999|  
|Intervalo de horas|00:00:00 a 23:59:59.997|  
|Intervalo de deslocamento de fuso horário|None|  
|Intervalos de elementos|AAAA são quatro dígitos de 1753 a 9999 que representam um ano.<br /><br /> MM são dois dígitos, variando de 01 a 12, que representam um mês do ano especificado.<br /><br /> DD são dois dígitos, variando de 01 a 31, dependendo do mês, que representam um dia do mês especificado.<br /><br /> hh são dois dígitos, variando de 00 a 23, que representam a hora.<br /><br /> mm são dois dígitos, variando de 00 a 59, que representam o minuto.<br /><br /> ss são dois dígitos, variando de 00 a 59, que representam o segundo.<br /><br /> n* vai de zero a três dígitos, variando de 0 a 999, representando as frações de segundo.|  
|Comprimento de caracteres|19 posições no mínimo e 23 no máximo|  
|Tamanho de armazenamento|8 bytes|  
|Precisão|Os valores são arredondados em incrementos de .000, .003 ou .007 segundos.|  
|Valor padrão|1900-01-01 00:00:00|  
|Calendário|Gregoriano (não inclui o intervalo completo de anos.)|  
|Precisão de segundo fracionário definida pelo usuário|não|  
|Preservação e reconhecimento de deslocamento de fuso horário|não|  
|Reconhecimento de horário de verão|não|  
  
## <a name="supported-string-literal-formats-for-datetime"></a>Formatos de literais de cadeia de caracteres com suporte para datetime  
As tabelas a seguir listam os formatos de literais de cadeia de caracteres com suporte para **datetime**. Exceto para ODBC, os literais de cadeia de caracteres **datetime** estão entre aspas simples ('), por exemplo, 'string_literaL'. Se o ambiente não for **us_english**, os literais de cadeia de caracteres deverão estar no formato N'string_literaL'.
  
|Numérico|Descrição|  
|---|---|
|Formatos de data:<br /><br /> [0]4/15/[19]96--(mda)<br /><br /> [0]4-15-[19]96 -- (mda)<br /><br /> [0]4.15.[19]96 -- (mda)<br /><br /> [0]4/[19]96/15 -- (mad)<br /><br /> 15/[0]4/[19]96 -- (dma)<br /><br /> 15/[19]96/[0]4 -- (dam)<br /><br /> [19]96/15/[0]4 -- (adm)<br /><br /> [19]96/[0]4/15 -- (amd)<br /><br /> Formatos de hora:<br /><br /> 14:30<br /><br /> 14:30[:20:999]<br /><br /> 14:30[:20.9]<br /><br /> 4am<br /><br /> 4 PM|Você pode especificar dados de data com um mês numérico especificado. Por exemplo, 5/20/97 representa o vigésimo dia de maio de 1997. Ao usar um formato de data numérico, especifique o mês, o dia e o ano em uma cadeia de caracteres com barras (/), hífens (-) ou pontos (.) como separadores. Essa cadeia de caracteres deve ser exibida da seguinte forma:<br /><br /> *número separador número separador número [time] [time]*<br /><br /> <br /><br /> Quando o idioma é definido como **us_english**, a ordem padrão da data é mdy. Você pode alterar a ordem da data usando a instrução [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md).<br /><br /> A configuração de SET DATEFORMAT determina como são interpretados os valores de data. Se a ordem não corresponder à configuração, os valores não serão interpretados como datas, porque eles estarão fora do intervalo ou serão mal-interpretados. Por exemplo, 12/10/08 pode ser interpretada como uma de seis datas, dependendo da configuração DATEFORMAT. Um ano de quatro partes é interpretado como o ano.|  
  
|Em ordem alfabética|Descrição|  
|---|---|
|Apr[il] [15][,] 1996<br /><br /> Apr[il] 15[,] [19]96<br /><br /> Apr[il] 1996 [15]<br /><br /> [15] Apr[il][,] 1996<br /><br /> 15 Apr[il][,][19]96<br /><br /> 15 [19]96 apr[il]<br /><br /> [15] 1996 apr[il]<br /><br /> 1996 APR[IL] [15]<br /><br /> 1996 [15] APR[IL]|Você pode especificar dados de data com um mês especificado como o nome de mês cheio. Por exemplo, abril ou a abreviação Apr especificadas na linguagem atual; vírgulas são opcionais e não há diferenciação entre letras maiúsculas e minúsculas.<br /><br /> Aqui estão algumas diretrizes para o uso de formatos de data alfabéticos:<br /><br /> 1) Insira os dados de data e hora com aspas simples ('). Para idiomas diferentes de inglês, use N'<br /><br /> 2) Os caracteres entre colchetes são opcionais.<br /><br /> 3) Se você especificar apenas os dois últimos dígitos do ano, os valores menores que os dois últimos dígitos do valor da opção de configuração [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) estarão no mesmo século do ano de corte. Os valores maiores ou iguais ao valor dessa opção estão no século anterior ao ano de corte. Por exemplo, se **two digit year cutoff** for 2050 (padrão), 25 será interpretado como 2025 e 50 será interpretado como 1950. Para evitar ambiguidade, use anos de quatro dígitos.<br /><br /> 4) Se o dia estiver ausente, o primeiro dia do mês será fornecido.<br /><br /> <br /><br /> A configuração de sessão SET DATEFORMAT não é aplicada quando você especifica o mês de forma alfabética.|  
  
|ISO 8601|Descrição|  
|---|---|
|AAAA-MM-DDThh:mm:ss[.mmm]<br /><br /> AAAAMMDD[ hh:mm:ss[.mmm]]|Exemplos:<br /><br /> 1) 2004-05-23T14:25:10<br /><br /> 2) 2004-05-23T14:25:10.487<br /><br /> <br /><br /> Para usar o formato ISO 8601, você deve especificar cada elemento no formato. Isto também inclui o **T**, os dois pontos (:) e o ponto final (.) que são mostrados no formato.<br /><br /> Os parênteses indicam que o componente de fração de segundo é opcional. O componente de hora é especificado no formato de 24 horas.<br /><br /> O T indica o início da parte de hora do valor de **datetime**.<br /><br /> A vantagem de usar o formato ISO 8601 é que ele é um padrão internacional com especificação não ambígua. Além disso, esse formato não é afetado pela configuração SET DATEFORMAT ou [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).|  
  
|Não separado|Descrição|  
|---|---|
|AAAAMMDDThh:mm:ss[.mmm]||  
  
|ODBC|Descrição|  
|---|---|
|{ ts '1998-05-02 01:23:56.123' }<br /><br /> { d '1990-10-02' }<br /><br /> { t '13:33:41' }|A API ODBC define sequências de escape para representar valores de data e hora que o ODBC chama de dados de carimbo de data/hora. Também há suporte para esse formato de carimbo de data/hora do ODBC na definição de idioma OLE DB (DBGUID-SQL) compatível com o provedor OLE DB do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os aplicativos que usam ADO, OLE DB e as APIs baseadas em ODBC podem usar esse formato de carimbo de data/hora de ODBC para representar datas e horas.<br /><br /> As sequências de escape do carimbo de data/hora do ODBC estão no formato: { *literal_type* '*constant_value*' }:<br /><br /> <br /><br /> - *literal_type* especifica o tipo da sequência de escape. Os carimbos de data/hora têm três especificadores de *literal_type*:<br />1) d = somente data<br />2) t = somente hora<br />3) ts = carimbo de data/hora (hora + data)<br /><br /> <br /><br /> - '*constant_value*' é o valor da sequência de escape. *constant_value* deve seguir esses formatos para cada *literal_type*.<br />d: yyyy-mm-dd<br />t: hh:mm:ss[.fff]<br />ts: yyyy-mm-dd hh:mm:ss[.fff]|  
  
## <a name="rounding-of-datetime-fractional-second-precision"></a>Arredondando a precisão de segundo fracionário de datetime  
Os valores de **datetime** são arredondados em incrementos de .000, .003 ou .007 segundos, como mostrado na tabela a seguir.
  
|Valor especificado pelo usuário|Valor armazenado pelo sistema|  
|---|---|
|01/01/98 23:59:59.999|1998-01-02 00:00:00.000|  
|01/01/98 23:59:59.995<br /><br /> 01/01/98 23:59:59.996<br /><br /> 01/01/98 23:59:59.997<br /><br /> 01/01/98 23:59:59.998|1998-01-01 23:59:59.997|  
|01/01/98 23:59:59.992<br /><br /> 01/01/98 23:59:59.993<br /><br /> 01/01/98 23:59:59.994|1998-01-01 23:59:59.993|  
|01/01/98 23:59:59.990<br /><br /> 01/01/98 23:59:59.991|1998-01-01 23:59:59.990|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Conformidade com ANSI e ISO 8601  
**datetime** não está em conformidade com o ANSI ou ISO 8601.
  
##  <a name="_datetime"></a> Convertendo dados de data e hora  
Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com os dados de data e hora, consulte [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-other-date-and-time-types-to-the-datetime-data-type"></a>Convertendo outros tipos de data e hora no tipo de dados datetime 
Esta seção descreve o que acontece quando outros tipos de dados de data e hora são convertidos no tipo de dados **datetime**.  
  
Quando a conversão é de **date**, o ano, mês e dia são copiados. O componente de hora é definido como 00:00:00.000. O código a seguir mostra os resultados da conversão de um valor `date` em um valor `datetime`.  
  
```sql
DECLARE @date date = '12-21-16';  
DECLARE @datetime datetime = @date;  
  
SELECT @datetime AS '@datetime', @date AS '@date';  
  
--Result  
--@datetime               @date  
------------------------- ----------  
--2016-12-21 00:00:00.000 2016-12-21  
```  
  
Quando a conversão é de **time(n)**, o componente de hora é copiado e o componente de data é definido como '1900-01-01'. Quando a precisão fracionária do valor de **time(n)** for maior que três dígitos, o valor será truncado para ser ajustado. O exemplo a seguir mostra os resultados da conversão de um valor `time(4)` em um valor `datetime`.  
  
```sql
DECLARE @time time(4) = '12:10:05.1237';  
DECLARE @datetime datetime = @time;  
  
SELECT @datetime AS '@datetime', @time AS '@time';  
  
--Result  
--@datetime               @time  
------------------------- -------------  
--1900-01-01 12:10:05.123 12:10:05.1237  
```  
  
Quando a conversão é de **smalldatetime**, as horas e os minutos são copiados. Os segundos e as frações de segundo são definidos como 0. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `datetime`.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @datetime AS '@datetime', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetime               @smalldatetime  
------------------------- -----------------------  
--2016-12-01 12:32:00.000 2016-12-01 12:32:00  
```  
  
Quando a conversão é de **datetimeoffset(n)**, os componentes de data e hora são copiados. O fuso horário é truncado. Quando a precisão fracionária do valor de **datetimeoffset(n)** for maior que três dígitos, o valor será truncado. O exemplo a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `datetime`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1968-10-23 12:45:37.1234 +10:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetime AS '@datetime', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@datetime               @datetimeoffset  
------------------------- ------------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237 +01:0   
```  
  
Quando a conversão é de **datetime2(n)**, a data e hora são copiadas. Quando a precisão fracionária do valor de **datetime2(n)** for maior que três dígitos, o valor será truncado. O exemplo a seguir mostra os resultados da conversão de um valor `datetime2(4)` em um valor `datetime`.  
  
```sql
DECLARE @datetime2 datetime2(4) = '1968-10-23 12:45:37.1237';  
DECLARE @datetime datetime = @datetime2;  
  
SELECT @datetime AS '@datetime', @datetime2 AS '@datetime2';  
  
--Result  
--@datetime               @datetime2  
------------------------- ------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237  
```  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir compara os resultados da conversão de uma cadeia de caracteres em cada tipo de dados **date** e **time**.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|Tipo de dados|Saída|  
|---|---|
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
