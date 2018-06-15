---
title: date (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- date_TSQL
- date
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], date
- date and time [SQL Server], date
- dates [SQL Server], data types
- date data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: c963e8b4-5a85-4bd0-9d48-3f8da8f6516b
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 792774360e368f0cf950cacfd97a8c2d5355e8e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33055213"
---
# <a name="date-transact-sql"></a>data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define uma data no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
## <a name="date-description"></a>Descrição de date
  
|Propriedade|Valor|  
|--------------|-----------|  
|Sintaxe|**date**|  
|Uso|DECLARE @MyDate **date**<br /><br /> CREATE TABLE Table1 ( Column1 **date** )|  
|Formato literal de cadeia de caracteres padrão<br /><br /> (usado para cliente de nível inferior)|AAAA-MM-DD<br /><br /> Para obter mais informações, consulte a seção Compatibilidade com versões anteriores a seguir.|  
|Intervalo|0001-01-01 a 9999-12-31 (1582-10-15 a 9999-12-31 para o Informatica)<br /><br /> 1 de janeiro de 1 CE até 31 de dezembro de 9999 CE (15 de outubro de 1582 CE a 31 de dezembro de 9999 CE para o Informatica)|  
|Intervalos de elementos|AAAA são quatro dígitos de 0001 a 9999 que representam um ano. Para o Informatica, YYYY está limitado ao intervalo de 1582 a 9999.<br /><br /> MM são dois dígitos de 01 a 12 que representam um mês do ano especificado.<br /><br /> DD são dois dígitos de 01 a 31, dependendo do mês que representa um dia do mês especificado.|  
|Comprimento de caracteres|10 posições|  
|Precisão, escala|10, 0|  
|Tamanho de armazenamento|3 bytes, fixo.|  
|Estrutura de armazenamento|Um número inteiro de 1, 3 bytes armazena a data.|  
|Precisão|Um dia|  
|Valor padrão|1900-01-01<br /><br /> Esse valor é usado para a parte de data acrescentada para conversão implícita de **time** em **datetime2** ou **datetimeoffset**.|  
|Calendário|Gregoriano|  
|Precisão de segundo fracionário definida pelo usuário|não|  
|Preservação e reconhecimento de deslocamento de fuso horário|não|  
|Reconhecimento de horário de verão|não|  
  
## <a name="supported-string-literal-formats-for-date"></a>Formatos de literais de cadeia de caracteres compatíveis com date
A tabela a seguir mostra os formatos de literais de cadeia de caracteres válidos para o tipo de dados **date**.
  
|Numérico|Description|  
|-------------|-----------------|  
|mda<br /><br /> [m]m/dd/[aa]aa<br /><br /> [m]m-dd-[aa]aa<br /><br /> [m]m.dd.[aa]aa<br /><br /> mad<br /><br /> mm/[aa]aa/dd<br /><br /> mm-[aa]aa/dd<br /><br /> [m]m.[aa]aa.dd<br /><br /> dma<br /><br /> dd/[m]m/[aa]aa<br /><br /> dd-[m]m-[aa]aa<br /><br /> dd.[m]m.[aa]aa<br /><br /> dam<br /><br /> dd/[aa]aa/[m]m<br /><br /> dd-[aa]aa-[m]m<br /><br /> dd.[aa]aa.[m]m<br /><br /> amd<br /><br /> [aa]aa/[m]m/dd<br /><br /> [aa]aa-[m]m-dd<br /><br /> [aa]aa-[m]m-dd|[m]m, dd e [aa]aa representam o mês, o dia e o ano de uma cadeia de caracteres com barras (/), hífens (-), ou pontos (.) como separadores.<br /><br /> Somente anos de dois ou quatro dígitos possuem suporte. Use quatro dígitos para o ano sempre que possível. Para especificar um inteiro de 0001 até 9999 que representa o ano de corte para interpretar anos com dois dígitos como de quatro dígitos, use [Configurar a opção two digit year cutoff de configuração do servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).<br /><br /> **Observação!** Para o Informatica, YYYY está limitado ao intervalo de 1582 a 9999.<br /><br /> Um ano de dois dígitos que é menor ou igual aos últimos dois dígitos do ano de corte está no mesmo século do ano de corte. Um ano de dois dígitos que é maior ou igual aos últimos dois dígitos do ano de corte está no mesmo século que vem antes do ano de corte. Por exemplo, se o ano de corte de dois dígitos for 2049 padrão, o ano de dois dígitos 49 será interpretado como 2049 e o ano de dois dígitos 50 será interpretado como 1950.<br /><br /> Os formato padrão de data é determinado pelas configurações atuais de idioma. Você pode alterar o formato da data usando as instruções [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md).<br /><br /> O formato **ydm** não dá suporte a **date**.|  
  
|Em ordem alfabética|Description|  
|------------------|-----------------|  
|mês [dd][,] aaaa<br /><br /> mês dd[,] [aa]aa<br /><br /> mês aaaa [dd]<br /><br /> [dd] mês[,] aaaa<br /><br /> dd mês[,][aa]aa<br /><br /> dd [aa]aa mês<br /><br /> [dd] aaaa mês<br /><br /> aaaa mês [dd]<br /><br /> aaaa [dd] mês|**mon** representa o nome completo do mês ou a abreviação do mês fornecida no idioma atual. As vírgulas são opcionais e não há diferenciação entre letras maiúsculas e minúsculas.<br /><br /> Para evitar ambiguidade, use anos de quatro dígitos.<br /><br /> Se o dia estiver ausente, o primeiro dia do mês será fornecido.|  
  
|ISO 8601|Descrição|  
|--------------|----------------|  
|AAAA-MM-DD<br /><br /> AAAAMMDD|Igual ao padrão SQL. Este é o único formato que é definido como padrão internacional.|  
  
|Não separado|Description|  
|-----------------|-----------------|  
|[aa]aammdd<br /><br /> aaaa[mm][dd]|Os dados de **date** podem ser especificados com quatro, seis ou oito dígitos. Uma cadeia de caracteres de seis ou oito dígitos é sempre interpretada como **ymd**. O mês e o dia sempre devem ser de dois dígitos. Uma cadeia de caracteres de quatro dígitos é interpretada como um ano.|  
  
|ODBC|Description|  
|----------|-----------------|  
|{ d 'aaaa-mm-dd' }|Específico à API ODBC.|  
  
|Formato W3C XML|Description|  
|--------------------|-----------------|  
|aaaa-mm-ddTZD|Suporte específico para utilização com XML/SOAP.<br /><br /> TZD é o designador de fuso horário (Z ou + hh: mm ou -hh:mm):<br /><br /> -   hh:mm representa o deslocamento de fuso horário. hh são dois dígitos, variando de 0 a 14, que representam o número de horas no deslocamento de fuso horário.<br />-   MM são dois dígitos, variando de 0 a 59, que representam o número de minutos adicionais no deslocamento de fuso horário.<br />-   + (mais) ou – (menos) é o sinal obrigatório do deslocamento de fuso horário. Ele indica que o deslocamento de fuso horário é adicionado ou subtraído do UTC (Tempo Universal Coordenado) para se obter a hora local. O intervalo válido de deslocamento de fuso horário vai de -14: 00 a +14: 00.|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Conformidade com o ANSI e ISO 8601  
**date** é compatível com a definição do padrão ANSI SQL do calendário Gregoriano: "NOTA 85 – Tipos de dados date e time aceitarão que datas no formato Gregoriano sejam armazenadas no intervalo de data 0001-01-01 CE a 9999-12-31 CE".
  
O formato padrão de literais de cadeia de caracteres que é usado para clientes de nível inferior,é compatível com o formato padrão SQL que é definido como AAAA-MM-DD. Este formato é o mesmo da definição ISO 8601 para DATE.
  
> [!NOTE]  
>  Para o Informatica, o intervalo é limitado a 1582-10-15 (15 de outubro de 1582 CE) a 9999-12-31 (31 de dezembro de 9999 CE).  
  
## <a name="backward-compatibility-for-down-level-clients"></a>Compatibilidade com versões anteriores de clientes de nível inferior
Alguns clientes de nível inferior não dão suporte aos tipos de dados **time**, **date**, **datetime2** e **datetimeoffset**. A tabela a seguir mostra o mapeamento de tipos entre uma instância de nível superior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clientes de nível inferior.
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Formato de literal de cadeia de caracteres padrão passado ao cliente de nível inferior|ODBC de nível inferior|OLEDB de nível inferior|JDBC de nível inferior|SQLCLIENT de nível inferior|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**date**|AAAA-MM-DD|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR ou SQL_VARCHAR|DBTYPE_WSTR ou DBTYPE_STR|Java.sql.String|Cadeia de caracteres ou SqString|  
  
## <a name="converting-date-and-time-data"></a>Convertendo dados de data e hora
Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com os dados de data e hora, consulte [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
### <a name="converting-date-to-other-date-and-time-types"></a>Convertendo date em outros tipos de data e hora
A tabela a seguir descreve o que ocorre quando um tipo de dados **date** é convertido em outros tipos de dados de data e hora.
  
Quando a conversão é para **time(n)**, a conversão falha e a mensagem de erro 206 é gerada: "Conflito no tipo de operando: a data é incompatível com a hora".
  
Se a conversão é feita em **datetime**, a data é copiada. O código a seguir mostra os resultados da conversão de um valor `date` em um valor `datetime`.
  
```sql
DECLARE @date date= '12-10-25';  
DECLARE @datetime datetime= @date;  
  
SELECT @date AS '@date', @datetime AS '@datetime';  
  
--Result  
--@date      @datetime  
------------ -----------------------  
--2025-12-10 2025-12-10 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
Quando a conversão é feita em uma **smalldatetime**, o valor de **date**está no intervalo de uma [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), o componente de data é copiado e o componente de hora é definido como 00:00:00.000. Quando o valor de **date** está fora do intervalo de um valor de **smalldatetime**, a mensagem de erro 242 é gerada: "A conversão de um tipo de dados date em um tipo de dados smalldatetime resultou em um valor fora do intervalo". Além disso, o valor de **smalldatetime** é definido como NULL. O código a seguir mostra os resultados da conversão de um valor `date` em um valor `smalldatetime`.
  
```sql
DECLARE @date date= '1912-10-25';  
DECLARE @smalldatetime smalldatetime = @date;  
  
SELECT @date AS '@date', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@date      @smalldatetime  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00  
--  
--(1 row(s) affected)  
```  
  
Para a conversão em **datetimeoffset(n)**, a data é copiada e a hora é definida como 00:00.0000000 +00:00. O código a seguir mostra os resultados da conversão de um valor `date` em um valor `datetimeoffset(3)`.
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetimeoffset datetimeoffset(3) = @date;  
  
SELECT @date AS '@date', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@date      @datetimeoffset  
------------ ------------------------------  
--1912-10-25 1912-10-25 00:00:00.000 +00:00  
--  
--(1 row(s) affected)  
```  
  
Quando a conversão é feita em **datetime2(n)**, o componente de data é copiado e o componente de hora é definido como 00:00.000000. O código a seguir mostra os resultados da conversão de um valor `date` em um valor `datetime2(3)`.
  
```sql
DECLARE @date date = '1912-10-25'  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-date"></a>Convertendo literais de cadeias de caracteres em data
Serão permitidas conversões de literais de cadeia de caracteres para tipos de data e hora se todas as partes da cadeia de caracteres estiverem em formatos válidos. Caso contrário, será gerado um erro de tempo de execução. As conversões implícitas ou explícitas que não especificam um estilo, de tipos de data e hora em literais de cadeia de caracteres estarão no formato padrão da sessão atual. A tabela a seguir mostra as regras de conversão de uma literal de cadeia de caracteres no tipo de dados **date**.
  
|Literal de cadeia de caracteres de entrada|**date**|  
|---|---|
|ODBC DATE|Os literais de cadeia de caracteres do ODBC são mapeados para o tipo de dados **datetime**. Qualquer operação de atribuição de literais de ODBC DATETIME em um tipo **date** causará uma conversão implícita entre **datetime** e esse tipo, conforme definido pelas regras de conversão.|  
|ODBC TIME|Consulte a regra de ODBC DATE anterior.|  
|ODBC DATETIME|Consulte a regra de ODBC DATE anterior.|  
|Apenas DATE|Trivial|  
|Apenas TIME|Os valores padrão são fornecidos.|  
|Apenas TIMEZONE|Os valores padrão são fornecidos.|  
|DATE + TIME|A parte DATE da cadeia de caracteres de entrada é usada.|  
|DATE + TIMEZONE|Não permitido.|  
|TIME + TIMEZONE|Os valores padrão são fornecidos.|  
|DATE + TIME + TIMEZONE|A parte DATE de DATETIME local será usada.|  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir compara os resultados da conversão de uma cadeia de caracteres para cada tipo de dados de data e hora.
  
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
|---------------|------------|  
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
