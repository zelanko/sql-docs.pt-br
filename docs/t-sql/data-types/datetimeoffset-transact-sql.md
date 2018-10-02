---
title: datetimeoffset (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- datetimeoffset_TSQL
- datetimeoffset
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetimeoffset
- datetimeoffset data type [SQL Server]
- dates [SQL Server], data types
- data types [SQL Server], date and time
- time zones [SQL Server]
ms.assetid: a0455b71-ca25-476e-a7a8-0770f1860bb7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 966b2acdeff68d445935b55ea1bf8ab24f2ad74a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684694"
---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define a data combinada com uma hora de um dia que possui reconhecimento de fuso horário e é baseada em um relógio de 24 horas.
  
## <a name="datetimeoffset-description"></a>Descrição de datetimeoffset
  
|Propriedade|Valor|  
|---|---|
|Sintaxe|**datetimeoffset** [ (*precisão de segundos fracionários*) ]|  
|Uso|DECLARE \@MyDatetimeoffset **datetimeoffset(7)**<br /><br /> CREATE TABLE Table1 ( Column1 **datetimeoffset(7)** )|  
|Formatos de literal de cadeia de caracteres padrão (usados para cliente de nível inferior)|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+&#124;-}hh:mm]<br /><br /> Para obter mais informações, consulte a seção Compatibilidade com versões anteriores a seguir.|  
|Intervalo de datas|0001-01-01 a 9999-12-31<br /><br /> 1 de janeiro de 1 CE até 31 de dezembro de 9999 CE|  
|Intervalo de horas|00:00:00 a 23:59:59.9999999 (não há suporte para segundos fracionários no Informatica)|  
|Intervalo de deslocamento de fuso horário|-14h00 a +14h00 (o deslocamento de fuso horário é ignorado no Informatica)|  
|Intervalos de elementos|AAAA são quatro dígitos, variando de 0001 a 9999, que representam um ano.<br /><br /> MM são dois dígitos, variando de 01 a 12, que representam um mês do ano especificado.<br /><br /> DD são dois dígitos, variando de 01 a 31, dependendo do mês, que representam um dia do mês especificado.<br /><br /> hh são dois dígitos, variando de 00 a 23, que representam a hora.<br /><br /> mm são dois dígitos, variando de 00 a 59, que representam o minuto.<br /><br /> ss são dois dígitos, variando de 00 a 59, que representam o segundo.<br /><br /> n* é de zero a sete dígitos, variando de 0 a 9999999, que representa as frações de segundo. Não há suporte para segundos fracionários no Informatica.<br /><br /> hh são dois dígitos que abrangem de -14 a +14. O deslocamento de fuso horário é ignorado no Informatica.<br /><br /> mm são dois dígitos que abrangem de 00 a 59. O deslocamento de fuso horário é ignorado no Informatica.|  
|Comprimento de caracteres|Mínimo de 26 posições (YYYY-MM-DD hh:mm:ss {+&#124;-}hh:mm) até um máximo de 34 (YYYY-MM-DD hh:mm:ss.nnnnnnn {+&#124;-}hh:mm)|  
|Precisão, escala|Veja a tabela abaixo.|  
|Tamanho de armazenamento|10 bytes, fixos, é o padrão com o padrão de precisão de segundos fracionários de 100ns.|  
|Precisão|100 nanossegundos|  
|Valor padrão|1900-01-01 00:00:00 00:00|  
|Calendário|Gregoriano|  
|Precisão de segundo fracionário definida pelo usuário|Sim|  
|Preservação e reconhecimento de deslocamento de fuso horário|Sim|  
|Reconhecimento de horário de verão|não|  
  
|Escala especificada|Resultado (precisão, escala)|Comprimento de coluna (bytes)|Precisão de segundos fracionários|  
|---|---|---|---|
|**datetimeoffset**|(34.7)|10|7|  
|**datetimeoffset(0)**|(26.0)|8|0-2|  
|**datetimeoffset(1)**|(28.1)|8|0-2|  
|**datetimeoffset(2)**|(29.2)|8|0-2|  
|**datetimeoffset(3)**|(30.3)|9|3-4|  
|**datetimeoffset(4)**|(31.4)|9|3-4|  
|**datetimeoffset(5)**|(32.5)|10|5-7|  
|**datetimeoffset(6)**|(33.6)|10|5-7|  
|**datetimeoffset(7)**|(34.7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>Formatos de literal de cadeia de caracteres compatíveis com datetimeoffset
A tabela a seguir lista os formatos de literal de cadeia de caracteres ISO 8601 compatíveis com **datetimeoffset**. Para obter informações sobre os formatos alfabéticos, numéricos, não separados e de hora para as partes de data e hora de **datetimeoffset**, consulte [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md) e [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Descrição|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.nnnnnnn][{+&#124;-}hh:mm]|Esses dois formatos não são afetados pelas configurações de localidade de sessão SET LANGUAGE e SET DATEFORMAT. Não são permitidos espaços entre as partes **datetimeoffset** e **datetime**.|  
|AAAA-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|Esse formato, pela definição ISO, indica que a parte de **datetime** deve ser expressa em UTC (Tempo Universal Coordenado). Por exemplo, 1999-12-12 12:30:30.12345 -07:00 deve ser representado como 1999-12-12 19:30:30.12345Z.|  
  
## <a name="time-zone-offset"></a>Deslocamento de fuso horário
Um deslocamento de fuso horário especifica o deslocamento de fuso horário de UTC para um valor de **time** ou **datetime**. O deslocamento de fuso horário pode ser representado como [+|-] hh:mm:
-   hh são dois dígitos, que abrangem de 00 a 14, que representam o número de horas no deslocamento de fuso horário.  
-   mm são dois dígitos, variando de 00 a 59, que representam o número de minutos adicionais no deslocamento de fuso horário.  
-   \+ (mais) ou – (menos) são sinais obrigatórios em um deslocamento de fuso horário. Indicam se o deslocamento de fuso horário é adicionado ou subtraído da hora UTC para se obter a hora local. O intervalo válido de deslocamento de fuso horário vai de -14: 00 a +14: 00.  
  
O intervalo de deslocamento de fuso horário segue o padrão W3C XML para definição de esquema XSD e é ligeiramente diferente da definição padrão do SQL 2003, 12:59 a +14:00.
  
A *precisão de segundos fracionários* do parâmetro de tipo opcional especifica o número de dígitos para a parte fracionária dos segundos. Esse valor pode ser um número inteiro com 0 a 7 (100 nanossegundos). A *precisão de segundos fracionários* padrão é 100ns (sete dígitos para a parte fracionária dos segundos).
  
Os dados são armazenados no banco de dados e processados, comparados, classificados e indexados no servidor como em UTC. O deslocamento de fuso horário será preservado no banco de dados para recuperação.
  
O deslocamento de fuso horário especificado será considerado como tendo reconhecimento de DST (horário de verão) e ajustado para qualquer **datetime** fornecida que estiver no período de DST.
  
Para o tipo **datetimeoffset**, tanto o UTC quanto o valor de **datetime** local (para o deslocamento de fuso horário persistente ou convertido) serão validados durante as operações de inserção, atualização, aritméticas, conversão ou atribuição. A detecção de qualquer valor de **datetime** UTC ou local inválido (para o deslocamento de fuso horário persistente ou convertido) causará um erro de valor inválido. Por exemplo, 9999-12-31 10:10:00 é válido no UTC, mas excede em hora local para o deslocamento de fuso horário em +13:50.
  
Para converter uma data em um valor de **datetimeoffset** correspondente em um fuso horário de destino, consulte [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>Conformidade com o ANSI e ISO 8601  
As seções de conformidade com o ANSI e ISO 8601 dos tópicos de [date](../../t-sql/data-types/date-transact-sql.md) e [time](../../t-sql/data-types/time-transact-sql.md) se aplicam a **datetimeoffset**.
  
## <a name="backward-compatibility-for-down-level-clients"></a>Compatibilidade com versões anteriores de clientes de nível inferior
Alguns clientes de nível inferior não dão suporte aos tipos de dados **time**, **date**, **datetime2** e **datetimeoffset**. A tabela a seguir mostra o mapeamento de tipos entre uma instância de nível superior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clientes de nível inferior.
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Formato de literal de cadeia de caracteres padrão passado ao cliente de nível inferior|ODBC de nível inferior|OLEDB de nível inferior|JDBC de nível inferior|SQLCLIENT de nível inferior|  
|---|---|---|---|---|---|
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**date**|AAAA-MM-DD|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
  
## <a name="converting-date-and-time-data"></a>Convertendo dados de data e hora
Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com os dados de data e hora, consulte [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>Convertendo tipo de dados datetimeoffset em outros tipos de data e hora
A seção a seguir descreve o que ocorre quando um tipo de dados **datetimeoffset** é convertido em outros tipos de dados de data e hora.
  
Ao fazer uma conversão em **date**, o ano, o mês e o dia são copiados. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `date`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10 +01:00';  
DECLARE @date date= @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @date AS 'date';  
  
--Result  
--@datetimeoffset                date  
-------------------------------- ----------  
--2025-12-10 12:32:10.0000 +01:0 2025-12-10  
--  
--(1 row(s) affected)  
  
```  
  
Se a conversão for feita em **time(n)**, a hora, o minuto, os segundos e os segundos fracionários serão copiados. O valor de fuso horário é truncado. Quando a precisão do valor de **datetimeoffset(n)** é maior que valor de **time(n)**, o valor é arredondado. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `time(3)`.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @time time(3) = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @time AS 'time';  
  
--Result  
--@datetimeoffset                time  
-------------------------------- ------------  
-- 2025-12-10 12:32:10.1237 +01:00    12:32:10.124  
  
--  
--(1 row(s) affected)  
  
```  
  
Ao fazer a conversão em **datetime**, os valores de data e hora são copiados e o fuso horário é truncado. Quando a precisão fracionária do valor de **datetimeoffset(n)** é maior que três dígitos, o valor é truncado. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `datetime`.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @datetime AS 'datetime';  
  
--Result  
--@datetimeoffset                datetime  
-------------------------------- -----------------------  
--2025-12-10 12:32:10.1237 +01:0 2025-12-10 12:32:10.123  
--  
--(1 row(s) affected)  
```  
  
Para conversões em **smalldatetime**, a data e a hora são copiadas. Os minutos são arredondados em relação ao valor dos segundos e os segundos são definidos como 0. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(3)` em um valor `smalldatetime`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(3) = '1912-10-25 12:24:32 +10:0';  
DECLARE @smalldatetime smalldatetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetimeoffset                @smalldatetime  
-------------------------------- -----------------------  
--1912-10-25 12:24:32.000 +10:00 1912-10-25 12:25:00  
--  
--(1 row(s) affected)  
```  
  
Se a conversão for feita em **datetime2(n)**, a data e a hora serão copiadas para o valor de **datetime2** e o fuso horário será truncado. Quando a precisão do valor de **datetime2(n)** é maior que a precisão do valor de **datetimeoffset(n)**, os segundos fracionários são truncados para serem ajustados. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `datetime2(3)`.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1912-10-25 12:24:32.1277 +10:0';  
DECLARE @datetime2 datetime2(3)=@datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @datetime2 AS '@datetime2';  
  
--Result  
@datetimeoffset                    @datetime2  
---------------------------------- ----------------------  
1912-10-25 12:24:32.1277 +10:00    1912-10-25 12:24:32.12  
  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-datetimeoffset"></a>Convertendo literais de cadeia de caracteres em datetimeoffset
Serão permitidas conversões de literais de cadeia de caracteres para tipos de data e hora se todas as partes da cadeia de caracteres estiverem em formatos válidos. Caso contrário, será gerado um erro de tempo de execução. As conversões implícitas ou explícitas que não especificam um estilo, de tipos de data e hora em literais de cadeia de caracteres estarão no formato padrão da sessão atual. A tabela a seguir mostra as regras de conversão de uma literal de cadeia de caracteres no tipo de dados **datetimeoffset**.
  
|Literal de cadeia de caracteres de entrada|**datetimeoffset(n)**|  
|---|---|
|ODBC DATE|Os literais de cadeia de caracteres do ODBC são mapeados para o tipo de dados **datetime**. Qualquer operação de atribuição de literais de ODBC DATETIME em tipos **datetimeoffset** causará uma conversão implícita entre **datetime** e esse tipo, conforme definido pelas regras de conversão.|  
|ODBC TIME|Consulte a regra de ODBC DATE anterior.|  
|ODBC DATETIME|Consulte a regra de ODBC DATE anterior.|  
|Apenas DATE|A parte TIME assume 00:00:00 como padrão. TIMEZONE assume +00:00 como padrão.|  
|Apenas TIME|A parte DATE assume 1900-1-1 como padrão. TIMEZONE assumirá +00:00 como padrão.|  
|Apenas TIMEZONE|Os valores padrão são fornecidos|  
|DATE + TIME|TIMEZONE assume +00:00 como padrão.|  
|DATE + TIMEZONE|Não permitido|  
|TIME + TIMEZONE|A parte DATE assume 1900-1-1 como padrão.|  
|DATE + TIME + TIMEZONE|Trivial|  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir compara os resultados da conversão de uma cadeia de caracteres em cada tipo de dados **date** e **time**.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset'  
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetimeoffset(7)) AS  
        'datetimeoffset IS08601';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|Tipo de dados|Saída|  
|---|---|
|**Time**|12:35:29. 1234567|  
|**Date**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**Datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**Datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  
