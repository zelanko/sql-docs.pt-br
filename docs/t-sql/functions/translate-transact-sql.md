---
title: Traduzir (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 583c414206a0acc79d1abdfff34728c38711a855
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="translate-transact-sql"></a>Traduzir (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Retorna a cadeia de caracteres fornecida como um primeiro argumento depois de alguns caracteres especificadas no segundo argumento são convertidos em um conjunto de caracteres de destino.

## <a name="syntax"></a>Sintaxe   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>Argumentos   

inputString   
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de caractere (nvarchar, varchar, nchar, char).

Caracteres   
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de caractere que contém caracteres que devem ser substituídos.

traduções   
É um caractere [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que coincida com o segundo argumento por tipo e comprimento.

## <a name="return-types"></a>Tipos de retorno   
Retorna uma expressão de caractere do mesmo tipo como `inputString` onde os caracteres do segundo argumento são substituídos com os caracteres de correspondência de terceiro argumento.

## <a name="remarks"></a>Comentários   

`TRANSLATE`função retornará um erro se os caracteres e traduções têm tamanhos diferentes. `TRANSLATE`função deve retornar entrada inalterada se valores nulos são fornecidos como argumentos de substituição ou caracteres. O comportamento do `TRANSLATE` função deve ser idêntica de [substituir](../../t-sql/functions/replace-transact-sql.md) função.   

O comportamento do `TRANSLATE` função é equivalente a usar vários `REPLACE` funções.

`TRANSLATE`é sempre o agrupamento de SC ciente.

## <a name="examples"></a>Exemplos   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. Substituir chaves quadrados e chaves com chaves regulares    
A consulta a seguir substitui chaves quadrados e chaves na cadeia de entrada entre parênteses:
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  O `TRANSLATE` função neste exemplo é equivalente a mas muito simplier que a instrução usando a seguinte `REPLACE`:`SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. Converter os pontos GeoJSON WKT    
GeoJSON é um formato de codificação de uma variedade de estruturas de dados geográficos. Com o `TRANSLATE` função, os desenvolvedores podem converter facilmente os pontos GeoJSON em formato WKT e vice-versa. A consulta a seguir substitui o quadrado e as chaves na entrada com chaves regulares:   
```tsql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|Ponto  |Coordenadas |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>Consulte também

[Funções de cadeia de caracteres (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[Substituir (Transact-SQL)](../../t-sql/functions/replace-transact-sql.md)   


