---
title: TRANSLATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 374e9c1ba9bd93900e8a6677984f5e0e63a7c454
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173593"
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Retorna a cadeia de caracteres fornecida como um primeiro argumento após a conversão de alguns caracteres especificados no segundo argumento em um conjunto de caracteres de destino especificado no terceiro argumento.

## <a name="syntax"></a>Sintaxe

```sql
TRANSLATE ( inputString, characters, translations)
```

## <a name="arguments"></a>Argumentos

 *inputString* É a [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de cadeia de caracteres a ser pesquisada. *inputString* pode ser qualquer tipo de dados de caractere (nvarchar, varchar, nchar, char).

 *characters* É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de cadeia de caracteres que contém caracteres que devem ser substituídos. *caracteres* pode ser qualquer tipo de dados de caractere.

*translations* É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de cadeia de caracteres que contém os caracteres de substituição. *translations* deve ser do mesmo tipo de dados e comprimento de *characters*.

## <a name="return-types"></a>Tipos de retorno

Retorna uma expressão de caractere do mesmo tipo de dados que `inputString`, em que os caracteres do segundo argumento são substituídos pelos caracteres correspondentes do terceiro argumento.

## <a name="remarks"></a>Comentários

`TRANSLATE` retornará um erro se as expressões *characters* e *translations* tiverem tamanhos diferentes. `TRANSLATE` retornará NULL se qualquer um dos argumentos for NULL.  

O comportamento da função `TRANSLATE` é semelhante ao uso de várias funções [REPLACE](../../t-sql/functions/replace-transact-sql.md). `TRANSLATE`, no entanto, não substitui qualquer caractere individual em `inputString` mais de uma vez. Um valor no parâmetro `characters` pode substituir vários caracteres em `inputString`. 

Isso é diferente do comportamento de várias funções `REPLACE`, pois cada chamada de função substitui todos os caracteres relevantes, mesmo que eles tenham sido substituídos por uma chamada de função `REPLACE` aninhada anteriormente. 

`TRANSLATE` sempre reconhece a ordenação SC.

## <a name="examples"></a>Exemplos

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>a. Substituir chaves e colchetes por chaves normais

A seguinte consulta substitui chaves e colchetes na cadeia de entrada por parênteses:

```sql
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```plain_text
2*(3+4)/(7-2)
```

#### <a name="equivalent-calls-to-replace"></a>Chamadas equivalentes para REPLACE

Na instrução SELECT a seguir, há um grupo de quatro chamadas aninhadas para a função REPLACE. Esse grupo é equivalente a uma chamada feita para a função TRANSLATE no SELECT anterior:

```sql
SELECT
REPLACE
(
      REPLACE
      (
            REPLACE
            (
                  REPLACE
                  (
                        '2*[3+4]/{7-2}',
                        '[',
                        '('
                  ),
                  ']',
                  ')'
            ),
            '{',
            '('
      ),
      '}',
      ')'
);
```

### <a name="b-convert-geojson-points-into-wkt"></a>B. Converter pontos GeoJSON em WKT

GeoJSON é um formato de codificação de uma variedade de estruturas de dados geográficos. Com a função `TRANSLATE`, os desenvolvedores podem converter com facilidade pontos GeoJSON no formato WKT e vice-versa. A seguinte consulta substitui chaves e colchetes na entrada por chaves normais:

```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Point  |Coordenadas |  
|---------|--------- |
|(137.4 72.3) |[137.4, 72.3] |

### <a name="c-use-the-translate-function"></a>C. Use a função TRANSLATE

```sql
SELECT TRANSLATE('abcdef','abc','bcd') AS Translated,
       REPLACE(REPLACE(REPLACE('abcdef','a','b'),'b','c'),'c','d') AS Replaced;
```

Os resultados são:

| Traduzido | Substituído |  
| ---------|--------- |
| bcddef | ddddef |


## <a name="see-also"></a>Consulte Também

 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [Funções de cadeia de caracteres (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)
