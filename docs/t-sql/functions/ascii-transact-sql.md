---
title: ASCII (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2c65df1f005b3d624f6a56f689f4125ec8175a7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="ascii-transact-sql"></a>ASCII (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o valor do código ASCII do caractere mais à esquerda de uma expressão de caractere.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASCII ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*character_expression*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **char** ou **varchar**.
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Comentários
ASCII é uma abreviação de código padrão americano para intercâmbio de informações. É um padrão usado por computadores de codificação de caracteres. Para obter uma lista de caracteres ASCII, consulte o **caracteres imprimíveis** seção [ASCII](https://www.wikipedia.org/wiki/ASCII).

## <a name="examples"></a>Exemplos  
O exemplo a seguir supõe um conjunto de caracteres ASCII e retorna o `ASCII` valor de 6 caracteres.
  
```sql
SELECT ASCII('A') AS A, ASCII('B') AS B,   
ASCII('a') AS a, ASCII('b') AS b,  
ASCII(1) AS [1], ASCII(2) AS [2];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
A           B           a           b           1           2  
----------- ----------- ----------- ----------- ----------- -----------  
65          66          97          98          49          50  
```  
  
## <a name="see-also"></a>Consulte também
[Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  



