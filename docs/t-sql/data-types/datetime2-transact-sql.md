---
title: datetime2 (Transact-SQL) | Microsoft Docs
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
- datetime2
- datetime2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- dates [SQL Server], data types
- date and time [SQL Server], datetime2
- data types [SQL Server], date and time
- datetime2 data type [SQL Server]
ms.assetid: 868017f3-214f-43ef-8536-cc1632a2288f
caps.latest.revision: 58
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13766b3d0cb86780c2eca55c7f36e8fd16e973c5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2-transact-sql"></a>datetime2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define uma data combinada com uma hora do dia que se baseia em um período de 24 horas. **datetime2** pode ser considerado como uma extensão existente **datetime** tipo que tem um intervalo de datas maior, uma precisão fracionária padrão mais e precisão opcional especificada pelo usuário.
  
## <a name="datetime2-description"></a>Descrição de datetime2
  
|Propriedade|Valor|  
|--------------|-----------|  
|Sintaxe|**datetime2** [(*precisão fracionária de segundos*)]|  
|Uso|DECLARAR @MyDatetime2 **datetime2 (7)**<br /><br /> Criar tabela Table1 (Column1 **datetime2 (7)** )|  
|Formato literal de cadeia de caracteres padrão<br /><br /> (usado para cliente de nível inferior)|YYYY-MM-DD hh:mm:ss[segundos fracionários]<br /><br /> Para obter mais informações, consulte a seção Compatibilidade com versões anteriores a seguir.|  
|Intervalo de datas|0001-01-01 a 9999-12-31<br /><br /> Janeiro 1,1 CE até 31 de dezembro de 9999 CE|  
|Intervalo de horas|00:00:00 a 23:59:59.9999999|  
|Intervalo de deslocamento de fuso horário|Nenhuma|  
|Intervalos de elementos|AAAA é um número de quatro dígitos, variando de 0001 a 9.999, que representa um ano.<br /><br /> MM é um número de dois dígitos, variando de 01 a 12 e representa um mês no ano especificado.<br /><br /> DD é um número de dois dígitos, variando de 01 a 31, dependendo do mês e representa um dia do mês especificado.<br /><br /> hh é um número de dois dígitos, variando de 00 a 23, que representa a hora.<br /><br /> mm é um número de dois dígitos, variando de 00 a 59, que representa o minuto.<br /><br /> ss é um número de dois dígitos, variando de 00 a 59, que representa o segundo.<br /><br /> n* é um número de zero a sete dígitos, variando de 0 a 9999999, que representa as frações de segundo. Em Informatica, as frações de segundo serão truncados quando n > 3.|  
|Comprimento de caracteres|19 posições no mínimo (YYYY-MM-DD hh:mm:ss ) a 27 no máximo (YYYY-MM-DD hh:mm:ss.0000000)|  
|Precisão, escala|0 a 7 dígitos, com exatidão de 100ns. A precisão padrão é 7 dígitos.|  
|Tamanho de armazenamento|6 bytes para precisões menores que 3; 7 bytes para precisões 3 e 4. Todas as outras precisões exigem 8 bytes.|  
|Precisão|100 nanossegundos|  
|Valor padrão|1900-01-01 00:00:00|  
|Calendário|Gregoriano|  
|Precisão de segundo fracionário definida pelo usuário|Sim|  
|Preservação e reconhecimento de deslocamento de fuso horário|Não|  
|Reconhecimento de horário de verão|Não|  
  
Para os metadados de tipo de dados, consulte [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md) ou [TYPEPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/typeproperty-transact-sql.md). Precisão e escala são variáveis para alguns tipos de data e data/hora. Para obter a precisão e escala de uma coluna, consulte [COLUMNPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/columnproperty-transact-sql.md), [COL_LENGTH &#40; Transact-SQL &#41; ](../../t-sql/functions/col-length-transact-sql.md), ou [Columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).
  
## <a name="supported-string-literal-formats-for-datetime2"></a>Suporte para formatos de literal de cadeia de caracteres para datetime2
As tabelas seguintes listam os formatos com suporte ISO 8601 e ODBC cadeia de caracteres literal para **datetime2**. Para obter informações sobre os formatos alfabéticos, numéricos, não separados e tempo para as partes de data e hora de **datetime2**, consulte [Data &#40; Transact-SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) e [tempo &#40; Transact-SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Descrições|  
|---|---|
|AAAA-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> AAAA-MM-DDThh:mm:ss[.nnnnnnn]|Esse formato não é afetado pelas configurações de localidade da sessão SET LANGUAGE e SET DATEFORMAT. O **T**, os dois-pontos (:) e o ponto (.) são incluídos na cadeia de caracteres literal, por exemplo ' 2007-05-02T19:58:47.1234567'.|  
  
|ODBC|Description|  
|---|---|
|{ ts 'yyyy-mm-dd hh:mm:ss[.segundos fracionários]' }|Específico de API ODBC:<br /><br /> O número de dígitos à esquerda do ponto decimal, que representa os segundos fracionários, pode ser especificado de 0 até 7 (100 nanossegundos).|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Conformidade com ANSI e ISO 8601  
A conformidade ANSI e ISO 8601 de [data](../../t-sql/data-types/date-transact-sql.md) e [tempo](../../t-sql/data-types/time-transact-sql.md) se aplicam a **datetime2**.
  
##  <a name="backward-compatibility-for-down-level-clients"></a>Compatibilidade com versões anteriores de clientes de nível inferior  
Alguns clientes de nível inferior não dão suporte a **tempo**, **data**, **datetime2** e **datetimeoffset** tipos de dados. A tabela a seguir mostra o mapeamento de tipos entre uma instância de nível superior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clientes de nível inferior.
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Formato de literal de cadeia de caracteres padrão passado ao cliente de nível inferior|ODBC de nível inferior|OLEDB de nível inferior|JDBC de nível inferior|SQLCLIENT de nível inferior|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**date**|AAAA-MM-DD|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetimeoffset**|AAAA-MM-DD HH [. nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
  
## <a name="converting-date-and-time-data"></a>Conversão de dados de data e hora
Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com dados de data e hora, consulte [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>Conversão de outros tipos de data e hora para o tipo de dados datetime2
Esta seção descreve o que acontece quando outros tipos de dados de data e hora são convertidos para o **datetime2** tipo de dados.  
  
Quando a conversão for de **data**, o ano, mês e dia são copiados.  O componente de hora é definido como 00:00:00.0000000.  O código a seguir mostra os resultados da conversão de um valor `date` em um valor `datetime2`.  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
Quando a conversão for de **time (n)**, o componente de hora é copiado e o componente de data é definido como ' 1900-01-01'. O exemplo a seguir mostra os resultados da conversão de um valor `time(7)` em um valor `datetime2`.  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
Quando a conversão for de **smalldatetime**, as horas e minutos são copiados. Os segundos e as frações de segundo são definidos como 0. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `datetime2`.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
Quando a conversão for de **DateTimeOffset (n)**, os componentes de data e hora são copiados. O fuso horário é truncado. O exemplo a seguir mostra os resultados da conversão de um valor `datetimeoffset(7)` em um valor `datetime2`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

Quando a conversão for de **datetime**, a data e hora são copiados.  A precisão fracionária é estendida para 7 dígitos.  O exemplo a seguir mostra os resultados da conversão de um valor `datetime` em um valor `datetime2`.

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  
  
### <a name="converting-string-literals-to-datetime2"></a>Convertendo literais de cadeia de caracteres em datetime2  
Serão permitidas conversões de literais de cadeia de caracteres para tipos de data e hora se todas as partes da cadeia de caracteres estiverem em formatos válidos. Caso contrário, será gerado um erro de tempo de execução. As conversões implícitas ou explícitas que não especificam um estilo, de tipos de data e hora em literais de cadeia de caracteres estarão no formato padrão da sessão atual. A tabela a seguir mostra as regras para converter uma cadeia de caracteres literal para o **datetime2** tipo de dados.
  
|Literal de cadeia de caracteres de entrada|**datetime2**|  
|---|---|
|ODBC DATE|Literais de cadeia de caracteres ODBC são mapeados para o **datetime** tipo de dados. Qualquer operação de atribuição de literais de ODBC DATETIME em **datetime2** tipos fará com que uma conversão implícita entre **datetime** e esse tipo conforme definido pelas regras de conversão.|  
|ODBC TIME|Consulte a regra de ODBC DATE anterior.|  
|ODBC DATETIME|Consulte a regra de ODBC DATE anterior.|  
|Apenas DATE|A parte TIME assume 00:00:00 como padrão.|  
|Apenas TIME|A parte DATE assume 1900-1-1 como padrão.|  
|Apenas TIMEZONE|Os valores padrão são fornecidos.|  
|DATE + TIME|Trivial|  
|DATE + TIMEZONE|Não permitido.|  
|TIME + TIMEZONE|A parte DATE assume 1900-1-1 como padrão. A entrada TIMEZONE é ignorada.|  
|DATE + TIME + TIMEZONE|O DATETIME local será usado.|  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir compara os resultados da conversão de uma cadeia de caracteres para cada **data** e **tempo** tipo de dados.
  
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
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

