---
title: FORMAT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 46c7becb151b1942b411aefe337717172f207bb9
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna um valor formatado com o formato e a cultura opcional especificados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Use a função FORMAT para formatação com reconhecimento de localidade de valores de data/hora e número como cadeias de caracteres. Para conversões de tipos de dados gerais, use CAST ou CONVERT.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *value*  
 Expressão de um tipo de dados com suporte para formatação. Para obter uma lista de tipos válidos, consulte a tabela na seção Comentários.  
  
 *format*  
 **nvarchar** padrão de formato.  
  
 O *formato* argumento deve conter uma cadeia de formato válido do .NET Framework, como uma cadeia de caracteres de formato padrão (por exemplo, "C" ou "D") ou como um padrão de caracteres personalizados para datas e valores numéricos (por exemplo, "MMMM DD, yyyy (dddd)") . A formatação composta não tem suporte. Para obter uma explicação completa desses padrões de formatação, consulte a documentação do .NET Framework na cadeia de caracteres de formatação em geral, data e formatos de hora e formatos numéricos personalizados. Um bom ponto de partida é o tópico "[formatando tipos](http://go.microsoft.com/fwlink/?LinkId=211776)."  
  
 *culture*  
 Opcional **nvarchar** argumento que especifica uma cultura.  
  
 Se o *cultura* argumento não for fornecido, será usado o idioma da sessão atual. Esse idioma é definido implícita ou explicitamente com o uso da instrução SET LANGUAGE. *cultura* aceita qualquer cultura com suporte do .NET Framework como um argumento; ele não está limitado aos idiomas com suporte explícito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o *cultura* argumento não é válido, FORMAT gerará um erro.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar** ou nulo  
  
 O comprimento do valor de retorno é determinado pelo *formato*.  
  
## <a name="remarks"></a>Remarks  
 FORMAT retorna NULL para erros diferentes de um *cultura* não *válido*. Por exemplo, NULL será retornado se o valor especificado em *formato* não é válido.  
 
 A função FORMAT é não determinística.   
  
 FORMATO se baseia na presença do .NET Framework em tempo de execução CLR (Common Language).  
  
 Essa função não pode ser remota, pois ele depende da presença do CLR. Uma função remota que exige o CLR pode causar um erro no servidor remoto.  
  
 FORMATO depende de regras que determinam que devem ser substituídos dois-pontos e os períodos de formatação do CLR. Portanto, quando o formato de cadeia de caracteres (o segundo parâmetro) contém uma vírgula ou período, o vírgula ou período devem ser precedidas de barra invertida quando um valor de entrada (primeiro parâmetro) é do **tempo** tipo de dados. Consulte [d. FORMAT com tipos de dados de tempo](#ExampleD).  
  
 A tabela a seguir lista os tipos de dados aceitáveis para o *valor* argumento junto com seus tipos de mapeamento do .NET Framework.  
  
|Categoria|Tipo|Tipo .NET|  
|--------------|----------|---------------|  
|Numérico|bigint|Int64|  
|Numérico|int|Int32|  
|Numérico|smallint|Int16|  
|Numérico|tinyint|Byte|  
|Numérico|decimal|SqlDecimal|  
|Numérico|numeric|SqlDecimal|  
|Numérico|float|Double|  
|Numérico|real|Single|  
|Numérico|smallmoney|Decimal|  
|Numérico|money|Decimal|  
|Data e hora|date|DateTime|  
|Data e hora|time|TimeSpan|  
|Data e hora|datetime|DateTime|  
|Data e hora|smalldatetime|DateTime|  
|Data e hora|datetime2|DateTime|  
|Data e hora|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-format-example"></a>A. Exemplo de FORMAT simples  
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
 O exemplo a seguir mostra os valores numéricos da formatação especificando um formato personalizado. O exemplo supõe que a data atual for 27 de setembro de 2012. Para obter mais informações sobre esses e outros formatos personalizados, consulte [cadeias de caracteres de formato numérico personalizado](http://msdn.microsoft.com/library/0c899ak8.aspx).  
  
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
 O exemplo a seguir retorna 5 linhas do **currencyrate** tabela o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados. A coluna **EndOfDateRate** são armazenados como tipo **money** na tabela. Neste exemplo, a coluna é retornada sem formatação e formatada com a especificação do formato de número .NET, o formato Geral e os tipos de formato de Moeda. Para obter mais informações sobre esses e outros formatos numéricos, consulte [cadeias de caracteres de formato numérico padrão](http://msdn.microsoft.com/library/dwhawy9k.aspx).  
  
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
  
###  <a name="ExampleD"></a> D. FORMAT com tipos de dados de tempo  
 FORMAT retorna NULL nesses casos, porque `.` e `:` não são ignoradas.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 Format retorna uma cadeia de caracteres formatada porque o `.` e `:` são ignoradas.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
