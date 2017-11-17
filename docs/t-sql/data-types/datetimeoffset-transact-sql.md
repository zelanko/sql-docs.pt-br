---
title: DateTimeOffset (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a6c143380711d1af39a6c11f311e9ce3caf87c7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define a data combinada com uma hora de um dia que possui reconhecimento de fuso horário e é baseada em um relógio de 24 horas.
  
## <a name="datetimeoffset-description"></a>Descrição DateTimeOffset
  
|Propriedade|Valor|  
|---|---|
|Sintaxe|**DateTimeOffset** [(*precisão fracionária de segundos*)]|  
|Uso|DECLARAR @MyDatetimeoffset **datetimeoffset(7)**<br /><br /> Criar tabela Table1 (Column1 **datetimeoffset(7)** )|  
|Formatos de literal de cadeia de caracteres padrão (usados para cliente de nível inferior)|AAAA-MM-DD HH [. nnnnnnn] [{+ &#124;-} hh: mm]<br /><br /> Para obter mais informações, consulte a seção Compatibilidade com versões anteriores a seguir.|  
|Intervalo de datas|0001-01-01 a 9999-12-31<br /><br /> 1 de janeiro de 1 CE até 31 de dezembro de 9999 CE|  
|Intervalo de horas|00:00:00 por meio de 23:59:59.9999999 (segundos fracionários não têm suporte em Informatica)|  
|Intervalo de deslocamento de fuso horário|-14:00 a + 14:00 (deslocamento de fuso horário é ignorado em Informatica)|  
|Intervalos de elementos|AAAA são quatro dígitos, variando de 0001 a 9999, que representam um ano.<br /><br /> MM são dois dígitos, variando de 01 a 12, que representam um mês do ano especificado.<br /><br /> DD são dois dígitos, variando de 01 a 31, dependendo do mês, que representam um dia do mês especificado.<br /><br /> hh são dois dígitos, variando de 00 a 23, que representam a hora.<br /><br /> mm são dois dígitos, variando de 00 a 59, que representam o minuto.<br /><br /> ss são dois dígitos, variando de 00 a 59, que representam o segundo.<br /><br /> n* é de zero a sete dígitos, variando de 0 a 9999999, que representa as frações de segundo. Não há suporte para frações de segundos em Informatica.<br /><br /> hh são dois dígitos que abrangem de -14 a +14. O deslocamento de fuso horário é ignorado em Informatica.<br /><br /> mm são dois dígitos que abrangem de 00 a 59. O deslocamento de fuso horário é ignorado em Informatica.|  
|Comprimento de caracteres|26 posições no mínimo (AAAA-MM-DD HH {+ &#124;-} hh: mm) a 34 no máximo (. AAAA-MM-DD nnnnnnn {+ &#124;-} hh: mm)|  
|Precisão, escala|Consulte a tabela a seguir.|  
|Tamanho de armazenamento|10 bytes, fixos, é o padrão com o padrão de precisão de segundos fracionários de 100ns.|  
|Precisão|100 nanossegundos|  
|Valor padrão|1900-01-01 00:00:00 00:00|  
|Calendário|Gregoriano|  
|Precisão de segundo fracionário definida pelo usuário|Sim|  
|Preservação e reconhecimento de deslocamento de fuso horário|Sim|  
|Reconhecimento de horário de verão|Não|  
  
|Escala especificada|Resultado (precisão, escala)|Comprimento de coluna (bytes)|Precisão de segundos fracionários|  
|---|---|---|---|
|**datetimeoffset**|(34,7)|10|7|  
|**DateTimeOffset(0)**|(26,0)|8|0-2|  
|**DateTimeOffset(1)**|(28,1)|8|0-2|  
|**DateTimeOffset(2)**|(29,2)|8|0-2|  
|**DateTimeOffset(3)**|(30,3)|9|3-4|  
|**DateTimeOffset(4)**|(31,4)|9|3-4|  
|**DateTimeOffset(5)**|(32,5)|10|5-7|  
|**DateTimeOffset(6)**|(33,6)|10|5-7|  
|**DateTimeOffset(7)**|(34,7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>Suporte para formatos de literal de cadeia de caracteres para datetimeoffset
A tabela a seguir lista os formatos de literal de cadeia de caracteres com suporte do ISO 8601 para **datetimeoffset**. Para obter informações sobre os formatos alfabéticos, numéricos, não separados e tempo para as partes de data e hora de **datetimeoffset**, consulte [Data &#40; Transact-SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) e [tempo &#40; Transact-SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Description|  
|---|---|
|AAAA-MM-ddTHH [. nnnnnnn] [{+ &#124;-} hh: mm]|Esses dois formatos não são afetados pelas configurações de localidade de sessão SET LANGUAGE e SET DATEFORMAT. Não são permitidos espaços entre o **datetimeoffset** e **datetime** partes.|  
|AAAA-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|Esse formato, pela definição ISO indica o **datetime** parte deve ser expresso em tempo Universal Coordenado (UTC). Por exemplo, 1999-12-12 12:30:30.12345 -07:00 deve ser representado como 1999-12-12 19:30:30.12345Z.|  
  
## <a name="time-zone-offset"></a>Deslocamento de fuso horário
Um deslocamento de fuso horário Especifica o deslocamento de fuso do UTC para um **tempo** ou **datetime** valor. O deslocamento de fuso horário pode ser representado como [+|-] hh:mm:
-   hh são dois dígitos, que abrangem de 00 a 14, que representam o número de horas no deslocamento de fuso horário.  
-   mm são dois dígitos, variando de 00 a 59, que representam o número de minutos adicionais no deslocamento de fuso horário.  
-   \+(mais) ou – (menos) são sinais obrigatórios em um deslocamento de fuso horário. Indicam se o deslocamento de fuso horário é adicionado ou subtraído da hora UTC para se obter a hora local. O intervalo válido de deslocamento de fuso horário vai de -14: 00 a +14: 00.  
  
O intervalo de deslocamento de fuso horário segue o padrão W3C XML para definição de esquema XSD e é ligeiramente diferente da definição padrão do SQL 2003, 12:59 a +14:00.
  
O parâmetro de tipo opcional *precisão fracionária de segundos* Especifica o número de dígitos para a parte fracionária dos segundos. Esse valor pode ser um número inteiro com 0 a 7 (100 nanossegundos). O padrão *precisão fracionária de segundos* é 100ns (sete dígitos para a parte fracionária dos segundos).
  
Os dados são armazenados no banco de dados e processados, comparados, classificados e indexados no servidor como em UTC. O deslocamento de fuso horário será preservado no banco de dados para recuperação.
  
O deslocamento de fuso horário fornecido será considerado como horário de verão (DST) com suporte e ajustado para qualquer dado **datetime** que está no período de DST.
  
Para **datetimeoffset** digitar, UTC e local (para o deslocamento de fuso horário persistente ou convertido) **datetime** valor será validado durante insert, update, arithmetic, convert ou assign operações. A detecção de qualquer UTC inválido ou local (para o deslocamento de fuso horário persistente ou convertido) **datetime** valor irá gerar um erro de valor inválido. Por exemplo, 9999-12-31 10:10:00 é válido no UTC, mas excede em hora local para o deslocamento de fuso horário em +13:50.
  
Para converter uma data correspondente **datetimeoffset** valor em um destino de fuso horário, consulte [AT TIME ZONE &#40; Transact-SQL &#41; ](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>Conformidade com ANSI e ISO 8601  
As seções ANSI e ISO 8601 conformidade do [data](../../t-sql/data-types/date-transact-sql.md) e [tempo](../../t-sql/data-types/time-transact-sql.md) tópicos se aplicam a **datetimeoffset**.
  
## <a name="backward-compatibility-for-down-level-clients"></a>Compatibilidade com versões anteriores de clientes de nível inferior
Alguns clientes de nível inferior não dão suporte a **tempo**, **data**, **datetime2** e **datetimeoffset** tipos de dados. A tabela a seguir mostra o mapeamento de tipos entre uma instância de nível superior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clientes de nível inferior.
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Formato de literal de cadeia de caracteres padrão passado ao cliente de nível inferior|ODBC de nível inferior|OLEDB de nível inferior|JDBC de nível inferior|SQLCLIENT de nível inferior|  
|---|---|---|---|---|---|
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**date**|AAAA-MM-DD|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetimeoffset**|AAAA-MM-DD HH [. nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
  
## <a name="converting-date-and-time-data"></a>Conversão de dados de data e hora
Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com dados de data e hora, consulte [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
Ao converter para **data**, o ano, mês e dia são copiados. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `date`.  
  
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
  
Se a conversão é em **time (n)**, o nosso, minuto, segundo e frações de segundo são copiados. O valor de fuso horário é truncado. Quando a precisão do **DateTimeOffset (n)** valor é maior que a precisão o **time (n)** , o valor é arredondado. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `time(3)`.
  
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
  
Ao converter para**datetime**, os valores de data e hora são copiados e o fuso horário é truncado. Quando a precisão fracionária de **DateTimeOffset (n)** valor é maior do que três dígitos, o valor é truncado. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `datetime`.
  
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
  
Para conversões em **smalldatetime**, a data e horário é copiados. Os minutos são arredondados em relação ao valor dos segundos e os segundos são definidos como 0. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(3)` em um valor `smalldatetime`.  
  
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
  
Se a conversão é em **datetime2**, a data e hora são copiados para o **datetime2** valor e o fuso horário é truncado. Quando a precisão do **datetime2** valor é maior que a precisão o **DateTimeOffset (n)** valor, os segundos fracionários são truncados para se ajustar. O código a seguir mostra os resultados da conversão de um valor `datetimeoffset(4)` em um valor `datetime2(3)`.
  
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
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>Conversão de tipo de dados datetimeoffset em outros data e tipos de tempo
A tabela a seguir descreve o que ocorre quando um **datetimeoffset** tipo de dados é convertido em outros tipos de dados de data e hora.
  
### <a name="converting-string-literals-to-datetimeoffset"></a>Convertendo literais de cadeia de caracteres em datetimeoffset
Serão permitidas conversões de literais de cadeia de caracteres para tipos de data e hora se todas as partes da cadeia de caracteres estiverem em formatos válidos. Caso contrário, será gerado um erro de tempo de execução. As conversões implícitas ou explícitas que não especificam um estilo, de tipos de data e hora em literais de cadeia de caracteres estarão no formato padrão da sessão atual. A tabela a seguir mostra as regras para converter uma cadeia de caracteres literal para o **datetimeoffset** tipo de dados.
  
|Literal de cadeia de caracteres de entrada|**DateTimeOffset (n)**|  
|---|---|
|ODBC DATE|Literais de cadeia de caracteres ODBC são mapeados para o **datetime** tipo de dados. Qualquer operação de atribuição de literais de ODBC DATETIME em **datetimeoffset** tipos fará com que uma conversão implícita entre **datetime** e esse tipo conforme definido pelas regras de conversão.|  
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
O exemplo a seguir compara os resultados da conversão de uma cadeia de caracteres para cada **data** e **tempo** tipo de dados.
  
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
|**Hora**|12:35:29. 1234567|  
|**Data**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**Datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**DateTimeOffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[FUSO horário &AMP; #40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  

