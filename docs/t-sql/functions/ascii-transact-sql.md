---
title: ASCII (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASCII_TSQL
- ASCII
dev_langs:
- TSQL
helpviewer_keywords:
- ASCII function
- characters [SQL Server], ASCII
- code [SQL Server], ASCII
- leftmost character of expression
ms.assetid: 45c2044a-0593-4805-8bae-0fad4bde2e6b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b982d357668703a54b06124a8bb3edf0c963463
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74119192"
---
# <a name="ascii-transact-sql"></a>ASCII (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o valor do código ASCII do caractere mais à esquerda de uma expressão de caractere.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASCII ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*character_expression*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **char** ou **varchar**.
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Comentários
ASCII significa **A**merican **S**tandard **C**ode for **I**nformation **I**nterchange. Ela serve como um padrão de codificação de caractere para computadores modernos. Veja a seção **Caracteres imprimíveis** do [ASCII](https://www.wikipedia.org/wiki/ASCII) para obter uma lista de caracteres ASCII.

ASCII é um conjunto de caracteres de 7 bits. ASCII estendido é um conjunto de caracteres de 8 bits que não é tratado pela função `ASCII`. 

## <a name="examples"></a>Exemplos 

### <a name="a-this-example-assumes-an-ascii-character-set-and-returns-the-ascii-value-for-6-characters"></a>a. Este exemplo pressupõe um conjunto de caracteres ASCII e retorna o valor `ASCII` para 6 caracteres.
  
```sql
SELECT ASCII('A') AS A, ASCII('B') AS B,   
ASCII('a') AS a, ASCII('b') AS b,  
ASCII(1) AS [1], ASCII(2) AS [2];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
A           B           a           b           1           2  
----------- ----------- ----------- ----------- ----------- -----------  
65          66          97          98          49          50  
```  
  
### <a name="b-this-examples-shows-how-a-7-bit-ascii-value-is-returned-correctly-but-an-8-bit-extended-ascii-value-is-not-handled"></a>B. Este exemplo mostra como um valor ASCII de 7 bits é retornado corretamente, mas um valor ASCII estendido de 8 bits não é tratado.

```sql
SELECT ASCII('P') AS [ASCII], ASCII('æ') AS [Extended_ASCII];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
ASCII       Extended_ASCII
----------- --------------
80          195
```

Para verificar se os resultados acima são mapeados para o ponto de código de caractere correto, use os valores de saída com a função `CHAR` ou `NCHAR`:

```sql
SELECT NCHAR(80) AS [CHARACTER], NCHAR(195) AS [CHARACTER];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
CHARACTER CHARACTER
--------- ---------
P         Ã
```

No resultado anterior, observe que o caractere para o ponto de código 195 é **Ã** e não **æ**. Isso ocorre porque a função `ASCII` pode ler o primeiro fluxo de 7 bits, mas não o bit extra. O ponto de código correto para o caractere `æ` pode ser encontrado usando a função `UNICODE`, que tem a capacidade de retornar o ponto de código de caractere correto:

```sql
SELECT UNICODE('æ') AS [Extended_ASCII], NCHAR(230) AS [CHARACTER];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
Extended_ASCII CHARACTER
-------------- ---------
230            æ
```

## <a name="see-also"></a>Confira também
 [CHAR &#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [UNICODE &#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
