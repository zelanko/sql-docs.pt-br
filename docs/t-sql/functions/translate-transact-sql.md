---
title: TRANSLATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ed5631256e47f38d2f329eafda4181190ab50c2
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068448"
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Retorna a cadeia de caracteres fornecida como um primeiro argumento após a conversão de alguns caracteres especificados no segundo argumento em um conjunto de caracteres de destino.

## <a name="syntax"></a>Sintaxe   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>Argumentos   

inputString   
É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de caractere (ou seja, nvarchar, varchar, nchar, char).

characters   
É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de um tipo de caractere que contém caracteres que devem ser substituídos.

traduções   
É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de caractere que corresponde ao segundo argumento por tipo e tamanho.

## <a name="return-types"></a>Tipos de retorno   
Retorna uma expressão de caractere do mesmo tipo que `inputString`, em que os caracteres do segundo argumento são substituídos pelos caracteres correspondentes do terceiro argumento.

## <a name="remarks"></a>Remarks   

A função `TRANSLATE` retornará um erro se os caracteres e as conversões tiverem tamanhos diferentes. A função `TRANSLATE` deverá retornar uma entrada inalterada se valores nulos forem fornecidos como argumentos de substituição ou caracteres. O comportamento da função `TRANSLATE` deve ser idêntico ao da função [REPLACE](../../t-sql/functions/replace-transact-sql.md).   

O comportamento da função `TRANSLATE` é equivalente ao uso de várias funções `REPLACE`.

`TRANSLATE` sempre reconhece o agrupamento SC.

## <a name="examples"></a>Exemplos   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. Substituir chaves e colchetes por chaves normais    
A seguinte consulta substitui chaves e colchetes na cadeia de entrada por parênteses:
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  A função `TRANSLATE` neste exemplo é equivalente à seguinte instrução using `REPLACE`, mas muito mais simples que ela: `SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. Converter pontos GeoJSON em WKT    
GeoJSON é um formato de codificação de uma variedade de estruturas de dados geográficos. Com a função `TRANSLATE`, os desenvolvedores podem converter com facilidade pontos GeoJSON no formato WKT e vice-versa. A seguinte consulta substitui chaves e colchetes na entrada por chaves normais:   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|Ponto  |Coordenadas |  
---------|--------- |
(137.4 72.3) |[137.4, 72.3] |


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

