---
title: datetime2 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c10e012010eb51973f3833573b09f0bb7e5fa18
ms.sourcegitcommit: 2da0c34f981c83d7f1d37435c80aea9d489724d1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782325"
---
# <a name="datetime2-transact-sql"></a>datetime2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define uma data combinada com uma hora do dia que se baseia em um período de 24 horas. **datetime2** pode ser considerada uma extensão do tipo **datetime** existente, que tem um intervalo maior de datas, uma precisão fracionária padrão mais ampla e precisão opcional especificada pelo usuário.
  
## <a name="datetime2-description"></a>Descrição de datetime2
  
|Propriedade|Valor|  
|--------------|-----------|  
|Sintaxe|**datetime2** [ (*precisão de segundos fracionários*) ]|  
|Uso|DECLARE \@MyDatetime2 **datetime2(7)**<br /><br /> CREATE TABLE Table1 ( Column1 **datetime2(7)** )|  
|Formato literal de cadeia de caracteres padrão<br /><br /> (usado para cliente de nível inferior)|YYYY-MM-DD hh:mm:ss[segundos fracionários]<br /><br /> Para obter mais informações, consulte a seção Compatibilidade com versões anteriores a seguir.|  
|Intervalo de datas|0001-01-01 a 9999-12-31<br /><br /> 1 de janeiro de 1 CE até 31 de dezembro de 9999 CE|  
|Intervalo de horas|00:00:00 a 23:59:59.9999999|  
|Intervalo de deslocamento de fuso horário|None|  
|Intervalos de elementos|AAAA é um número de quatro dígitos, variando de 0001 a 9.999, que representa um ano.<br /><br /> MM é um número de dois dígitos, variando de 01 a 12 e representa um mês no ano especificado.<br /><br /> DD é um número de dois dígitos, variando de 01 a 31, dependendo do mês e representa um dia do mês especificado.<br /><br /> hh é um número de dois dígitos, variando de 00 a 23, que representa a hora.<br /><br /> mm é um número de dois dígitos, variando de 00 a 59, que representa o minuto.<br /><br /> ss é um número de dois dígitos, variando de 00 a 59, que representa o segundo.<br /><br /> n* é um número de zero a sete dígitos, variando de 0 a 9999999, que representa as frações de segundo. No Informatica, os segundos fracionários serão truncados quando n > 3.|  
|Comprimento de caracteres|19 posições no mínimo (YYYY-MM-DD hh:mm:ss ) a 27 no máximo (YYYY-MM-DD hh:mm:ss.0000000)|  
|Precisão, escala|0 a 7 dígitos, com exatidão de 100ns. A precisão padrão é 7 dígitos.|  
|Tamanho de armazenamento|6 bytes para precisões menores que 3; 7 bytes para precisões 3 e 4. Todas as outras precisões exigem 8 bytes.|  
|Precisão|100 nanossegundos|  
|Valor padrão|1900-01-01 00:00:00|  
|Calendário|Gregoriano|  
|Precisão de segundo fracionário definida pelo usuário|Sim|  
|Preservação e reconhecimento de deslocamento de fuso horário|não|  
|Reconhecimento de horário de verão|não|  
  
Para obter os metadados de tipo de dados, consulte [sys.systypes &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md) ou [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md). Precisão e escala são variáveis para alguns tipos de data e data/hora. Para obter a precisão e escala de uma coluna, consulte [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md), [COL_LENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/col-length-transact-sql.md) ou [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).
  
## <a name="supported-string-literal-formats-for-datetime2"></a>Formatos de literal de cadeia de caracteres compatíveis com datetime2
As tabelas a seguir listam os formatos de literal de cadeia de caracteres ISO 8601 e ODBC para **datetime2**. Para obter informações sobre os formatos alfabéticos, numéricos, não separados e de hora para as partes de data e hora de **datetime2**, consulte [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md) e [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Descrições|  
|---|---|
|AAAA-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> AAAA-MM-DDThh:mm:ss[.nnnnnnn]|Esse formato não é afetado pelas configurações de localidade da sessão SET LANGUAGE e SET DATEFORMAT. O **T**, os dois pontos (:) e o ponto final (.) são incluídos no literal de cadeia de caracteres; por exemplo, '2007-05-02T19:58:47.1234567'.|  
  
|ODBC|Descrição|  
|---|---|
|{ ts 'yyyy-mm-dd hh:mm:ss[.segundos fracionários]' }|Específico de API ODBC:<br /><br /> O número de dígitos à esquerda do ponto decimal, que representa os segundos fracionários, pode ser especificado de 0 até 7 (100 nanossegundos).|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Conformidade com o ANSI e ISO 8601  
A conformidade com o ANSI e ISO 8601 de [date](../../t-sql/data-types/date-transact-sql.md) e [time](../../t-sql/data-types/time-transact-sql.md) se aplica a **datetime2**.
  
##  <a name="backward-compatibility-for-down-level-clients"></a>Compatibilidade com versões anteriores de clientes de nível inferior  
Alguns clientes de nível inferior não dão suporte aos tipos de dados **time**, **date**, **datetime2** e **datetimeoffset**. A tabela a seguir mostra o mapeamento de tipos entre uma instância de nível superior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clientes de nível inferior.
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Formato de literal de cadeia de caracteres padrão passado ao cliente de nível inferior|ODBC de nível inferior|OLEDB de nível inferior|JDBC de nível inferior|SQLCLIENT de nível inferior|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**date**|AAAA-MM-DD|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
  
## <a name="converting-date-and-time-data"></a>Convertendo dados de data e hora
Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com os dados de data e hora, consulte [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>Convertendo outros tipos de data e hora no tipo de dados datetime2
Esta seção descreve o que acontece quando outros tipos de dados de data e hora são convertidos no tipo de dados **datetime2**.  
  
Quando a conversão é de **date**, o ano, mês e dia são copiados.  O componente de hora é definido como 00:00:00.0000000.  O código a seguir mostra os resultados da conversão de um valor `date` em um valor `datetime2`.  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
Quando a conversão é de **time(n)**, o componente de hora é copiado e o componente de data é definido como '1900-01-01'. O exemplo a seguir mostra os resultados da conversão de um valor `time(7)` em um valor `datetime2`.  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
Quando a conversão é de **smalldatetime**, as horas e os minutos são copiados. Os segundos e as frações de segundo são definidos como 0. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `datetime2`.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
Quando a conversão é de **datetimeoffset(n)**, os componentes de data e hora são copiados. O fuso horário é truncado. O exemplo a seguir mostra os resultados da conversão de um valor `datetimeoffset(7)` em um valor `datetime2`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

Quando a conversão é de **datetime**, a data e hora são copiadas. A precisão fracionária é estendida para 7 dígitos. O exemplo a seguir mostra os resultados da conversão de um valor `datetime` em um valor `datetime2`.

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  

> [!NOTE]
> No nível de compatibilidade 130 do banco de dados, as conversões implícitas de tipos de dados datetime para datetime2 demonstram precisão aprimorada ao considerar os milissegundos fracionários. Isso resulta em diferentes valores convertidos, conforme visto no exemplo abaixo. Use conversão explícita para o tipo de dados datetime2 sempre que existir um cenário misto de comparação entre os tipos de dados datetime e datetime2. Para obter mais informações, consulte este [Artigo do Suporte da Microsoft](http://support.microsoft.com/help/4010261).

### <a name="converting-string-literals-to-datetime2"></a>Convertendo literais de cadeia de caracteres em datetime2  
Serão permitidas conversões de literais de cadeia de caracteres para tipos de data e hora se todas as partes da cadeia de caracteres estiverem em formatos válidos. Caso contrário, será gerado um erro de tempo de execução. As conversões implícitas ou explícitas que não especificam um estilo, de tipos de data e hora em literais de cadeia de caracteres estarão no formato padrão da sessão atual. A tabela a seguir mostra as regras de conversão de uma literal de cadeia de caracteres no tipo de dados **datetime2**.
  
|Literal de cadeia de caracteres de entrada|**datetime2(n)**|  
|---|---|
|ODBC DATE|Os literais de cadeia de caracteres do ODBC são mapeados para o tipo de dados **datetime**. Qualquer operação de atribuição de literais de ODBC DATETIME em tipos **datetime2** causará uma conversão implícita entre **datetime** e esse tipo, conforme definido pelas regras de conversão.|  
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
  
  
