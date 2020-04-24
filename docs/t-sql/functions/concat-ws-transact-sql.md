---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af7ce381b1a0fdef6db197e8e764d137cf641b7c
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635399"
---
# <a name="concat_ws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

Essa função retorna uma cadeia de caracteres resultante de concatenação ou junção de dois ou mais valores de cadeia de caracteres de ponta a ponta. Ele separa esses valores de cadeia de caracteres concatenados com o delimitador especificado no argumento da primeira função. (`CONCAT_WS` indica *concatenar com separador*.)

##  <a name="syntax"></a>Sintaxe   
```syntaxsql
CONCAT_WS ( separator, argument1, argument2 [, argumentN]... )
```

## <a name="arguments"></a>Argumentos   
separator  
Uma expressão de qualquer tipo de caractere (`char`, `nchar`, `nvarchar` ou `varchar`).

argument1, argument2, argument*N*  
Uma expressão de qualquer tipo.

## <a name="return-types"></a>Tipos de retorno
Um valor de cadeia de caracteres cujos comprimento e tipo dependem da entrada.

## <a name="remarks"></a>Comentários   
`CONCAT_WS` usa um número variável de argumentos de cadeia de caracteres e os concatena em uma única cadeia de caracteres. Ele separa esses valores de cadeia de caracteres concatenados com o delimitador especificado no argumento da primeira função. `CONCAT_WS` exige um argumento separador e um mínimo de dois outros argumentos de valor de cadeia de caracteres; caso contrário, `CONCAT_WS` gerará um erro. `CONCAT_WS` converte implicitamente todos os argumentos nos tipos de cadeia de caracteres antes da concatenação. 

A conversão implícita em cadeias de caracteres segue as regras existentes para conversões de tipo de dados. Veja [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md) para saber mais sobre conversões de tipo de dados e comportamento.

### <a name="treatment-of-null-values"></a>Tratamento de valores NULL

`CONCAT_WS` ignora a configuração `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}`.

Se `CONCAT_WS` receber argumentos com todos os valores nulo, retornará uma cadeia de caracteres vazia do tipo varchar(1).

`CONCAT_WS` ignora os valores nulos durante a concatenação e não adicionam o separador entre valores nulos. Portanto, `CONCAT_WS` pode tratar a concatenação de cadeias de caracteres que podem ter valores "em branco", por exemplo, um segundo campo de endereço. Veja o exemplo B para saber mais.

Se um cenário envolver valores nulos, separados por um delimitador, considere a função `ISNULL`. Veja o exemplo C para saber mais.

## <a name="examples"></a>Exemplos   

### <a name="a--concatenating-values-with-separator"></a>a.  Concatenando valores com separador
Este exemplo concatena três colunas da tabela sys.databases, separando-os com um `-`.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 – SIMPLE – NONE |
|2 – SIMPLE – NONE |
|3 – FULL – NONE |
|4 – SIMPLE – NONE |


### <a name="b--skipping-null-values"></a>B.  Ignorando valores NULL
Este exemplo ignora valores `NULL` na lista de argumentos.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  Gerando arquivo CSV da tabela
Este exemplo usa uma vírgula `,` como valor separador e adiciona o caractere de retorno de carro `char(13)` no formato de valores separados por coluna do conjunto de resultados.

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, recovery_model_desc, containment_desc), char(13)) AS DatabaseInfo
FROM sys.databases
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
DatabaseInfo
------------   
1,SIMPLE,NONE
2,SIMPLE,NONE
3,FULL,NONE 
4,SIMPLE,NONE 
```

CONCAT_WS ignora valores NULL nas colunas. Encapsule uma coluna anulável com a função `ISNULL` e forneça um valor padrão. Veja este exemplo para saber mais:

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>Confira também
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

