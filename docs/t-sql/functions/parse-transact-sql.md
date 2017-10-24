---
title: PARSE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSE
- PARSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PARSE function
ms.assetid: 6a2dbf10-f692-471b-9458-24d246963049
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b332b92c77340c9cc7f6276d28286e048b2b0f2b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="parse-transact-sql"></a>PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna o resultado de uma expressão, convertida no tipo de dados solicitado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *String_value*  
 **nvarchar**valor (4000) que representa o valor formatado para analisar no tipo de dados especificado.  
  
 *String_value* deve ser uma representação válida do tipo de dados solicitado, ou PARSE gera um erro.  
  
 *data_type*  
 Valor literal que representa o tipo de dados solicitado para o resultado.  
  
 *cultura*  
 Cadeia de caracteres opcional que identifica a cultura na qual *string_value* é formatado.  
  
 Se o *cultura* argumento não for fornecido, então será usado o idioma da sessão atual. Esse idioma é definido implícita ou explicitamente com o uso da instrução SET LANGUAGE. *cultura* aceita qualquer cultura com suporte do .NET Framework; ele não está limitado aos idiomas com suporte explícito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o *cultura* argumento não é válido, PARSE gerará um erro.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o resultado da expressão, convertida no tipo de dados solicitado.  
  
## <a name="remarks"></a>Comentários  
 Os valores nulos transmitidos como argumentos para PARSE são tratados de dois modos:  
  
1.  Se uma constante nula for transmitida, um erro ocorrerá. Um valor nulo não pode ser analisado em um tipo de dados diferente de maneira cultural.  
  
2.  Se um parâmetro com um valor nulo for transmitido no momento da execução, um valor nulo será retornado, para evitar o cancelamento do lote inteiro.  
  
 Use PARSE somente para converter de cadeia de caracteres em data/hora e tipos numéricos. Para conversões de tipos gerais, continue a usar CAST ou CONVERT. Lembre-se de que há uma certa sobrecarga de desempenho na análise do valor da cadeia de caracteres.  
  
 PARSE depende da presença do .NET Framework em tempo de execução CLR (Common Language).  
  
 Essa função não será remota uma vez que ela depende da presença do CLR. Uma função remota que exige o CLR provocará um erro no servidor remoto.  
  
 **Para obter mais informações sobre o parâmetro data_type**  
  
 Os valores para o *data_type* parâmetro são restritos aos tipos mostrados na tabela a seguir, junto com estilos. As informações de estilo são fornecidas para ajudar a determinar que tipos de padrões são permitidos. Para obter mais informações sobre estilos, consulte a documentação do .NET Framework para o **System.Globalization.NumberStyles** e **DateTimeStyles** enumerações.  
  
|Categoria|Tipo|Tipo de .NET Framework|Estilos usados|  
|--------------|----------|-------------------------|-----------------|  
|Numérico|bigint|Int64|NumberStyles.Number|  
|Numérico|int|Int32|NumberStyles.Number|  
|Numérico|smallint|Int16|NumberStyles.Number|  
|Numérico|tinyint|Byte|NumberStyles.Number|  
|Numérico|decimal|Decimal|NumberStyles.Number|  
|Numérico|numeric|Decimal|NumberStyles.Number|  
|Numérico|float|Double|NumberStyles.Float|  
|Numérico|real|Single|NumberStyles.Float|  
|Numérico|smallmoney|Decimal|NumberStyles.Currency|  
|Numérico|money|Decimal|NumberStyles.Currency|  
|Data e hora|date|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Data e hora|time|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Data e hora|datetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Data e hora|smalldatetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Data e hora|datetime2|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Data e hora|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
  
 **Para obter mais informações sobre o parâmetro de cultura**  
  
 A tabela a seguir mostra os mapeamentos de idiomas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para culturas do .NET Framework.  
  
|Nome completo|Alias|LCID|Cultura específica|  
|---------------|-----------|----------|----------------------|  
|us_english|Inglês|1046|pt-BR|  
|Deutsch|Alemão|1031|de-DE|  
|Français|Francês|1036|fr-FR|  
|日本語|Japonês|1041|ja-JP|  
|Dansk|Dinamarquês|1030|da-DK|  
|Español|Espanhol|3082|es-ES|  
|Italiano|Italiano|1040|it-IT|  
|Nederlands|Holandês|1043|nl-NL|  
|Norsk|Norueguês|2068|nn-NO|  
|Português|Português|2070|pt-PT|  
|Suomi|Finlandês|1035|fi|  
|Svenska|Sueco|1053|sv-SE|  
|Čeština|Tcheco|1029|Cs-CZ|  
|magyar|Húngaro|1038|Hu-HU|  
|polski|Polonês|1045|Pl-PL|  
|română|Romeno|1048|Ro-RO|  
|hrvatski|Croata|1050|hr-HR|  
|slovenčina|Eslovaco|1051|Sk-SK|  
|slovenski|Esloveno|1060|Sl-SI|  
|ΕΛΛΗΝΙΚΆ|Grego|1032|El-GR|  
|БЪЛГАРСКИ|Búlgaro|1026|bg-BG|  
|РУССКИЙ|Russo|1049|Ru-RU|  
|Türkçe|Turco|1055|Tr-TR|  
|British|British English|2057|en-GB|  
|eesti|Estoniano|1061|Et-EE|  
|latviešu|Letão|1062|lv-LV|  
|lietuvių|Lituano|1063|lt-LT|  
|Português (Brasil)|Português do Brasil|1046|pt-BR|  
|繁體中文|Chinês tradicional|1028|zh-TW|  
|한국어|Coreano|1042|Ko-KR|  
|简体中文|Chinês simplificado|2052|zh-CN|  
|Árabe|Árabe|1025|ar-SA|  
|ไทย|Tailandês|1054|Th-TH|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-parse-into-datetime2"></a>A. PARSE em datetime2  
  
```  
SELECT PARSE('Monday, 13 December 2010' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-13 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-parse-with-currency-symbol"></a>B. PARSE com símbolo de moeda  
  
```  
SELECT PARSE('€345,98' AS money USING 'de-DE') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
345.98  
  
(1 row(s) affected)  
```  
  
### <a name="c-parse-with-implicit-setting-of-language"></a>C. PARSE com configuração implícita de idioma  
  
```  
-- The English language is mapped to en-US specific culture  
SET LANGUAGE 'English';  
SELECT PARSE('12/16/2010' AS datetime2) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-16 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
  

