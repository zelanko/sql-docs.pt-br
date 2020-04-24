---
title: FORMAT (Transact-SQL) | Microsoft Docs
description: Referência de Transact-SQL para a função FORMAT.
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: b72089909596808dabb3c3f77359af5d8176a875
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81625589"
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

Retorna um valor formatado com o formato e a cultura opcional especificados. Use a função FORMAT para formatação com reconhecimento de localidade de valores de data/hora e número como cadeias de caracteres. Para conversões de tipos de dados gerais, use CAST ou CONVERT.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>Argumentos

 *value*  
 Expressão de um tipo de dados com suporte para formatação. Para obter uma lista de tipos válidos, consulte a tabela na seção Comentários.  
  
 *format*  
 Padrão de formato **nvarchar**.  
  
 O argumento *format* deve conter uma cadeia de formato válido do .NET Framework, como uma cadeia de formato padrão (por exemplo, "C" ou "D") ou como um padrão de caracteres personalizados para obter datas e valores numéricos (por exemplo, "MMMM DD, aaaa (dddd)"). A formatação composta não tem suporte. Para obter uma explicação completa sobre esses padrões de formatação, veja a documentação do .NET Framework sobre formatação de cadeias de caracteres em geral, formatos personalizados de data e hora e formatos personalizados de número. Um bom ponto de partida é o tópico, "[Formatando tipos](https://go.microsoft.com/fwlink/?LinkId=211776)".  
  
 *cultura*  
 Argumento **nvarchar** opcional especificando uma cultura.  
  
 Se o argumento *culture* não for fornecido, o idioma da sessão atual será usado. Esse idioma é definido implícita ou explicitamente com o uso da instrução SET LANGUAGE. *culture* aceita qualquer cultura compatível com .NET Framework como um argumento. Ela não é limitada aos idiomas explicitamente compatíveis com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o argumento *culture* não for válido, FORMAT gerará um erro.  
  
## <a name="return-types"></a>Tipos de retorno

 **nvarchar** ou nulo  
  
 A extensão do valor retornado é determinada pelo *format*.  
  
## <a name="remarks"></a>Comentários

 FORMAT retorna NULL para erros que não uma *cultura* que não é *valid*. Por exemplo, NULL será retornado se o valor especificado em *format* não for válido.  

 A função FORMAT é não determinística.
  
 FORMAT conta com a presença do CLR (Common Language Runtime) do .NET Framework.  
  
 Essa função não pode ser remota, uma vez que ela depende da presença do CLR. Tornar remota uma função que exige o CLR pode provocar um erro no servidor remoto.  
  
 FORMAT depende de regras de formatação CLR, que determinam que pontos e vírgulas e pontos finais devem ser ignorados. Portanto, quando a cadeia de caracteres de formato (segundo parâmetro) contém uma vírgula ou ponto, a vírgula ou o ponto devem ser precedidos por uma barra invertida quando um valor de entrada (primeiro parâmetro) é do tipo de dados **time**. Veja [D. FORMAT com tipos de dados de tempo](#ExampleD).  
  
 A tabela a seguir lista os tipos de dados aceitáveis para o argumento *value*, junto com os tipos equivalentes de mapeamento do .NET Framework.  
  
|Categoria|Type|Tipo .NET|  
|--------------|----------|---------------|  
|Numérico|BIGINT|Int64|  
|Numérico|INT|Int32|  
|Numérico|SMALLINT|Int16|  
|Numérico|TINYINT|Byte|  
|Numérico|decimal|SqlDecimal|  
|Numérico|numeric|SqlDecimal|  
|Numérico|FLOAT|Double|  
|Numérico|real|Single|  
|Numérico|SMALLMONEY|Decimal|  
|Numérico|money|Decimal|  
|Data e hora|date|Datetime|  
|Data e hora|time|TimeSpan|  
|Data e hora|DATETIME|Datetime|  
|Data e hora|smalldatetime|Datetime|  
|Data e hora|datetime2|Datetime|  
|Data e hora|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-format-example"></a>a. Exemplo de FORMAT simples

 O exemplo a seguir retorna uma data simples formatada para culturas diferentes.  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>B. FORMAT com cadeias de caracteres de formatação personalizadas

 O exemplo a seguir mostra os valores numéricos da formatação especificando um formato personalizado. O exemplo supõe que a data atual é 27 de setembro de 2012. Para obter mais informações sobre esses e outros formatos personalizados, veja [Cadeias de caracteres de formato numérico personalizado](https://msdn.microsoft.com/library/0c899ak8.aspx).  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>C. FORMAT com tipos numéricos

 O exemplo a seguir retorna 5 linhas da tabela **Sales.CurrencyRate** no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A coluna **EndOfDateRate** é armazenada como o tipo **money** na tabela. Neste exemplo, a coluna é retornada sem formatação e formatada com a especificação do formato de número .NET, o formato Geral e os tipos de formato de Moeda. Para obter mais informações sobre esses e outros formatos numéricos, veja [Cadeias de caracteres de formato numérico padrão](https://msdn.microsoft.com/library/dwhawy9k.aspx).  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 Este exemplo especifica a cultura alemã (de-de).  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
### <a name="d-format-with-time-data-types"></a><a name="ExampleD"></a> D. FORMAT com tipos de dados de tempo

 FORMAT retorna NULL nesses casos, porque `.` e `:` não são ignorados.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 Format retorna uma cadeia de caracteres formatada porque `.` e `:` são ignorados.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  

Format retorna uma hora atual formatada com AM ou PM especificado

```sql
SELECT FORMAT(SYSDATETIME(), N'hh:mm tt'); -- returns 03:46 PM
SELECT FORMAT(SYSDATETIME(), N'hh:mm t'); -- returns 03:46 P
```

Format retorna a hora especificada, exibindo AM

```sql
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm tt') -- returns 01:00 AM
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm t')  -- returns 01:00 A
```

Format retorna a hora especificada, exibindo PM

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm tt') -- returns 02:00 PM
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm t') -- returns 02:00 P
```
  
Format retorna a hora especificada em formato 24 h

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'HH:mm') -- returns 14:00
```
  
## <a name="see-also"></a>Consulte Também

 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
