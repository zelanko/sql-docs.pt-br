---
title: hora (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 6/7/2017
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
- time_TSQL
- time
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- time [SQL Server]
- date and time [SQL Server], time
- data types [SQL Server], date and time
- time data type [SQL Server]
ms.assetid: 30a6c681-8190-48e4-94d0-78182290a402
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4a5a46eee481e9da3f388f88e982d705dbe150ea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="time-transact-sql"></a>hora (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Define uma hora de um dia. A hora se encontra sem reconhecimento de fuso horário e se baseia em um relógio de 24 horas.  
  
  > [!NOTE]  
  > São fornecidas informações de Informatica para clientes do PDW usando o conector de Informatica. 
  
## <a name="time-description"></a>Descrição de time  
  
|Propriedade|Valor|  
|--------------|-----------|  
|Sintaxe|**tempo** [(*escala frações de segundo*)]|  
|Uso|DECLARAR @MyTime **time(7)**<br /><br /> Criar tabela Table1 (Column1 **time(7)** )|  
|*escala de frações de segundo*|Especifica o número de dígitos para a parte fracionária dos segundos.<br /><br /> Pode ser um inteiro de 0 a 7. Para Informatica, isso pode ser um inteiro de 0 a 3.<br /><br /> A escala de frações de padrão é 7 (100 NS).|  
|Formato literal de cadeia de caracteres padrão<br /><br /> (usado para cliente de nível inferior)|hh [. nnnnnnn] para Informatica)<br /><br /> Para obter mais informações, consulte a seção "Compatibilidade com versões anteriores de clientes de nível inferior" a seguir.|  
|Intervalo|00:00:00.0000000 por meio de 23:59:59.9999999 (00:00:00.000 por meio de 23:59:59.999 para Informatica)|  
|Intervalos de elementos|hh são dois dígitos, variando de 0 a 23, que representam a hora.<br /><br /> mm são dois dígitos, variando de 0 a 59, que representam o minuto.<br /><br /> ss são dois dígitos, variando de 0 a 59, que representam o segundo.<br /><br /> n\*é zero a sete dígitos, variando de 0 a 9999999, que representa as frações de segundo. Para Informatica, n\* é zero a três dígitos, variando de 0 a 999.|  
|Comprimento de caracteres|Mínimo de 8 posições (hh:mm:ss) até um máximo de 16 (hh:mm:ss.nnnnnnn) Para Informatica, o máximo é de 12 (hh:mm:ss.nnn).|  
|Precisão, escala<br /><br /> (usuário especifica apenas escala)|Consulte a tabela a seguir.|  
|Tamanho de armazenamento|5 bytes, fixos, são o padrão com o padrão de precisão de frações de segundo de 100 ns. Informatica, o padrão é 4 bytes, fixos, com o padrão de 1 MS fracionários precisão de segundo.|  
|Precisão|100 nanossegundos (1 milissegundo em Informatica)|  
|Valor padrão|00:00:00<br /><br /> Esse valor é usado para a parte de hora anexada para conversão implícita de **data** para **datetime2** ou **datetimeoffset**.|  
|Precisão de segundo fracionário definida pelo usuário|Sim|  
|Preservação e reconhecimento de deslocamento de fuso horário|Não|  
|Reconhecimento de horário de verão|Não|  
  
|Escala especificada|Resultado (precisão, escala)|Comprimento de coluna (bytes)|Fracionário<br /><br /> segundos<br /><br /> precisão|  
|---------------------|---------------------------------|-----------------------------|------------------------------------------|  
|**time**|(16,7) [Informatica em (12,3)]|5 (4 Informatica)|7 (3 em Informatica)|  
|**time(0)**|(8,0)|3|0-2|  
|**Time(1)**|(10,1)|3|0-2|  
|**Time(2)**|(11,2)|3|0-2|  
|**Time(3)**|(12,3)|4|3-4|  
|**Time(4)**<br /><br /> Não tem suporte no Informatica.|(13,4)|4|3-4|  
|**Time(5)**<br /><br /> Não tem suporte no Informatica.|(14,5)|5|5-7|  
|**Time(6)**<br /><br /> Não tem suporte no Informatica.|(15,6)|5|5-7|  
|**time(7)**<br /><br /> Não tem suporte no Informatica.|(16,7)|5|5-7|  
  
## <a name="supported-string-literal-formats-for-time"></a>Há suporte para formatos de literais de cadeia de caracteres para hora  
 A tabela a seguir mostra a cadeia de caracteres válida de formatos de literal para o **tempo** tipo de dados.  
  
|SQL Server|Description|  
|----------------|-----------------|  
|hh:mm[:ss][:segundos fracionários][AM][PM]<br /><br /> hh:mm[:ss][.segundos fracionários][AM][PM]<br /><br /> hhAM[PM]<br /><br /> hh AM [PM]|O valor de hora 0 representa a hora depois da meia-noite (AM), independentemente de AM ter sido especificado. PM não pode ser especificado quando a hora é igual a 0.<br /><br /> Os valores de hora de 01 a 11 representam as horas antes do meio-dia se não for especificado AM nem PM. Os valores também representam as horas antes do meio-dia quando AM é especificado. Os valores representarão as horas depois do meio-dia, se PM for especificado.<br /><br /> O valor de hora 12 representa a hora que começa ao meio-dia, se não for especificado AM nem PM. Se AM for especificado, o valor representará a hora que começa à meia-noite. Se PM for especificado, o valor representará a hora que começa ao meio-dia. Por exemplo, 12:01 é 1 minuto depois do meio-dia, assim como 12:01 PM; e 12:01 AM é 1 minuto depois da meia-noite. Especificar 12:01 AM é igual a especificar 00:01 ou 00:01 AM.<br /><br /> Os valores de hora de 13 a 23 representam as horas após o meio-dia, se AM nem PM estiverem especificados. Os valores também representam as horas após o meio-dia quando PM é especificado. AM não pode ser especificado quando o valor de hora é de 13 a 23.<br /><br /> Um valor de hora de 24 não é válido. Para representar meia-noite, use 12:00 AM ou 00:00.<br /><br /> Os milissegundos podem ser precedidos por ou dois-pontos (:) ou ponto (.). Se for usado dois-pontos, o número significa milésimos de segundo. Se for usado um ponto, um único dígito significa décimos de segundo, dois dígitos significa centésimos de segundo e três dígitos, milésimos de segundo. Por exemplo, 12:30:20:1 indica 20 e um milésimos de segundo após 12:30; 12:30:20.1 indica 20 e um décimos de segundo após 12:30.|  
  
|ISO 8601|Observações|  
|--------------|-----------|  
|hh:mm:ss<br /><br /> hh:mm[:ss][.segundos fracionários]|hh são dois dígitos, variando de 0 a 14, que representam o número de horas no deslocamento de fuso horário.<br /><br /> mm são dois dígitos, variando de 0 a 59, que representam o número de minutos adicionais no deslocamento de fuso horário.|  
  
|ODBC|Observações|  
|----------|-----------|  
|{t 'hh:mm:ss[.segundos fracionários]'}|Específico à API ODBC.|  
  
## <a name="compliance-with-ansi-and-iso-8601-standards"></a>Conformidade com os padrões ANSI e ISO 8601  
 Não há suporte para o uso da hora 24 para representar a meia-noite e saltar o segundo em 59, como definido pelo ISO 8601 (5.3.2 e 5.3), para a manutenção de compatibilidade retroativa e consistência com os tipos de data e hora existentes.  
  
 O formato de literais de cadeia de caracteres padrão (usado para cliente de nível inferior) se alinhará com o formulário padrão do SQL, que está definido como hh:mm:ss[.nnnnnnn]. Esse formato se assemelha à definição do ISO 8601 para TIME que exclui segundos fracionários.  
  
##  <a name="BackwardCompatibilityforDownlevelClients"></a>Compatibilidade com versões anteriores de clientes de nível inferior  
 Alguns clientes de nível inferior não dão suporte a **tempo**, **data**, **datetime2** e **datetimeoffset** tipos de dados. A tabela a seguir mostra o mapeamento de tipos entre uma instância de nível superior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clientes de nível inferior.  
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Formato de literal de cadeia de caracteres padrão passado ao cliente de nível inferior|ODBC de nível inferior|OLEDB de nível inferior|JDBC de nível inferior|SQLCLIENT de nível inferior|  
|-----------------------------------------|----------------------------------------------------------------|----------------------|-----------------------|----------------------|---------------------------|  
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**date**|AAAA-MM-DD|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetimeoffset**|AAAA-MM-DD HH [. nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
  
## <a name="converting-date-and-time-data"></a>Convertendo dados date e time  
 Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com dados de data e hora, consulte [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
### <a name="converting-timen-data-type-to-other-date-and-time-types"></a>Convertendo tipo de dados time(n) em outros tipos de data e hora  
 Esta seção descreve o que ocorre quando um **tempo** tipo de dados é convertido em outros tipos de dados de data e hora.  
  
 Quando a conversão é em **time (n)**, a hora, minutos e segundos são copiados. Quando a precisão de destino é menor do que a precisão de origem, as frações de segundo é arredondada para se ajustarem à precisão de destino. O exemplo a seguir mostra os resultados da conversão de um valor `time(4)` em um valor `time(3)`.  
  
```  
DECLARE @timeFrom time(4) = '12:34:54.1237';  
DECLARE @timeTo time(3) = @timeFrom;  
  
SELECT @timeTo AS 'time(3)', @timeFrom AS 'time(4)';  
  
--Results  
--time(3)      time(4)  
-------------- -------------  
--12:34:54.124 12:34:54.1237  
--  
--(1 row(s) affected)  
```  
  
 Se a conversão é em  
                    **data**, a conversão falhará e a mensagem de erro 206 é gerada: "conflito de tipo de operando: data é incompatível com a hora".  
  
 Quando a conversão é em **datetime**, hora, minuto e segundo valores são copiados e o componente de data é definido como ' 1900-01-01'. Quando a precisão fracionária de segundos do **time (n)** valor é maior do que três dígitos, o **datetime** resultado será truncado. O código a seguir mostra os resultados da conversão de um valor `time(4)` em um valor `datetime`.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime datetime= @time;  
SELECT @time AS '@time', @datetime AS '@datetime';  
  
--Result  
--@time         @datetime  
--------------- -----------------------  
--12:15:04.1237 1900-01-01 12:15:04.123  
--  
--(1 row(s) affected)  
  
```  
  
 Quando a conversão é em **smalldatetime**, a data é definida como ' 1900-01-01' e os valores de hora e minuto são arredondados. Os segundos e as frações de segundo são definidos como 0. O código a seguir mostra os resultados da conversão de um valor `time(4)` em um valor `smalldatetime`.  
  
```  
-- Shows rounding up of the minute value.  
DECLARE @time time(4) = '12:15:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';   
  
--Result  
@time            @smalldatetime  
---------------- -----------------------  
12:15:59.9999    1900-01-01 12:16:00--  
--(1 row(s) affected)  
  
-- Shows rounding up of the hour value.  
DECLARE @time time(4) = '12:59:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
  
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';  
@time            @smalldatetime  
---------------- -----------------------  
12:59:59.9999    1900-01-01 13:00:00  
  
(1 row(s) affected)  
  
```  
  
 Se a conversão é em **DateTimeOffset (n)**, a data é definida como ' 1900-01-01' e a hora é copiado. O deslocamento de fuso horário é definido como +00:00. Quando a precisão fracionária de segundos do **time (n)** valor é maior que a precisão do **DateTimeOffset (n)** , o valor é arredondado de acordo. O exemplo a seguir mostra os resultados da conversão de um valor `time(4)` em um tipo de valor `datetimeoffset(3)`.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetimeoffset datetimeoffset(3) = @time;  
  
SELECT @time AS '@time', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@time         @datetimeoffset  
--------------- ------------------------------  
--12:15:04.1237 1900-01-01 12:15:04.124 +00:00  
--  
--(1 row(s) affected)  
  
```  
  
 Ao converter para **datetime2**, a data é definida como ' 1900-01-01', o componente de hora é copiado e o deslocamento de fuso horário é definido como 00:00. Quando a precisão fracionária de segundos do **datetime2** valor é maior que o **time (n)** valor, o valor será arredondado para caber.  O exemplo a seguir mostra os resultados da conversão de um valor `time(4)` em um valor `datetime2(2)`.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime2 datetime2(3) = @time;  
  
SELECT @datetime2 AS '@datetime2', @time AS '@time';  
  
--Result  
--@datetime2              @time  
------------------------- -------------  
--1900-01-01 12:15:04.124 12:15:04.1237  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-timen"></a>Convertendo literais de cadeia de caracteres em time(n)  
 Serão permitidas conversões de literais de cadeia de caracteres para tipos de data e hora se todas as partes da cadeia de caracteres estiverem em formatos válidos. Caso contrário, será gerado um erro de tempo de execução. As conversões implícitas ou explícitas que não especificam um estilo, de tipos de data e hora em literais de cadeia de caracteres estarão no formato padrão da sessão atual. A tabela a seguir mostra as regras para converter uma cadeia de caracteres literal para o **tempo** tipo de dados.  
  
|Literal de cadeia de caracteres de entrada|Regra de conversão|  
|--------------------------|---------------------|  
|ODBC DATE|Literais de cadeia de caracteres ODBC são mapeados para o **datetime** tipo de dados. Qualquer operação de atribuição de literais de ODBC DATETIME em **tempo**tipos fará com que uma conversão implícita entre **datetime** e esse tipo conforme definido pelas regras de conversão.|  
|ODBC TIME|Consulte a regra ODBC DATE acima.|  
|ODBC DATETIME|Consulte a regra ODBC DATE acima.|  
|Apenas DATE|Os valores padrão são fornecidos.|  
|Apenas TIME|Trivial|  
|Apenas TIMEZONE|Os valores padrão são fornecidos.|  
|DATE + TIME|A parte TIME da cadeia de caracteres de entrada é usada.|  
|DATE + TIMEZONE|Não permitido.|  
|TIME + TIMEZONE|A parte TIME da cadeia de caracteres de entrada é usada.|  
|DATE + TIME + TIMEZONE|A parte TIME de DATETIME local será usada.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-comparing-date-and-time-data-types"></a>A. Comparando tipos de dados de data e hora  
 O exemplo a seguir compara os resultados da conversão de uma cadeia de caracteres para cada **data** e **tempo** tipo de dados.  
  
```  
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
  
|Tipo de dados|Saída|  
|---------------|------------|  
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
###  <a name="ExampleB"></a> B. Inserindo literais de cadeia de caracteres válidos na coluna time(7)  
 A tabela a seguir lista os literais de cadeia de caracteres diferentes que podem ser inseridos em uma coluna de tipo de dados **time(7)** com os valores que são armazenados na coluna.  
  
|Tipo de formato de literal de cadeia de caracteres|Literal de cadeia de caracteres inserido|valor de time(7) que é armazenado|Description|  
|--------------------------------|-----------------------------|------------------------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01:123AM'|01:01:01.1230000|Quando dois pontos (:) precedem a precisão de frações de segundo, a escala não pode exceder três posições ou ocorrerá um erro.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 AM'|1:01:01.1234567|Quando AM ou PM é especificado, a hora é armazenada em formato de 24 horas sem o literal AM ou PM|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 PM'|13:01:01.1234567|Quando AM ou PM é especificado, a hora é armazenada em formato de 24 horas sem o literal AM ou PM|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567PM'|13:01:01.1234567|Um espaço antes de AM ou PM é opcional.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:00:00'|01:00:00.0000000|Quando só a hora é especificada, todos os outros valores são 0.|  
|SQL Server|'01 AM'|01:00:00.0000000|Um espaço antes de AM ou PM é opcional.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01'|01:01:01.0000000|Quando a precisão das frações de segundo não é especificada, cada posição definida pelo tipo de dados é 0.|  
|ISO 8601|'01:01:01.1234567'|1:01:01.1234567|Para estar de acordo com o ISO 8601, use o formato de 24 horas, e não AM ou PM.|  
|ISO 8601|'01:01:01.1234567 +01:01'|1:01:01.1234567|A diferença de fuso horário (TZD) opcional é permitida na entrada, mas não é armazenada.|  
  
### <a name="c-inserting-time-string-literal-into-columns-of-each-date-and-time-date-type"></a>C. Inserindo o literal de cadeia de caracteres nas colunas de cada tipo de data e hora  
 Na tabela a seguir, a primeira coluna mostra um literal de cadeia de caracteres de hora a ser inserido em uma coluna da tabela do banco de dados do tipo de dados de data e hora exibido na segunda coluna. A terceira coluna mostra o valor que será armazenado na coluna da tabela do banco de dados.  
  
|Literal de cadeia de caracteres inserido|Tipo de dados da coluna|Valor que é armazenado na coluna|Description|  
|-----------------------------|----------------------|------------------------------------|-----------------|  
|'12:12:12.1234567'|**time(7)**|12:12:12.1234567|Se a precisão das frações de segundo exceder o valor especificado para a coluna, a cadeia de caracteres será truncada sem erro.|  
|'2007-05-07'|**date**|NULL|Qualquer valor de hora fará a instrução INSERT falhar.|  
|'12:12:12'|**smalldatetime**|1900-01-01 12:12:00|Qualquer valor de precisão de fração de segundo fará a instrução INSERT falhar.|  
|'12:12:12.123'|**datetime**|1900-01-01 12:12:12.123|Qualquer precisão de segundo mais extensa do que três posições fará a instrução INSERT falhar.|  
|'12:12:12.1234567'|**datetime2(7)**|1900-01-01 12:12:12.1234567|Se a precisão das frações de segundo exceder o valor especificado para a coluna, a cadeia de caracteres será truncada sem erro.|  
|'12:12:12.1234567'|**DateTimeOffset(7)**|1900-01-01 12:12:12.1234567 +00:00|Se a precisão das frações de segundo exceder o valor especificado para a coluna, a cadeia de caracteres será truncada sem erro.|  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
