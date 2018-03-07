---
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 88ba00513a8f76ae560ed717801150aa9b80046e
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Remove o caractere de espaço `char(32)` ou outros caracteres especificados do início ou término de uma cadeia de caracteres.  
 
## <a name="syntax"></a>Sintaxe   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[AMBOS | À ESQUERDA | À direita] não ainda disponível."

## <a name="arguments"></a>Argumentos   

Caracteres   
É um literal, uma variável ou uma chamada de função de qualquer tipo de caractere não LOB (`nvarchar`, `varchar`, `nchar`, ou `char`) que contém caracteres que devem ser removidos. `nvarchar(max)`e `varchar(max)` tipos não são permitidos.

cadeia de caracteres   
É uma expressão de qualquer tipo de caractere (`nvarchar`, `varchar`, `nchar`, ou `char`) onde os caracteres devem ser removidos.

## <a name="return-types"></a>Tipos de retorno   
Retorna uma expressão de caractere com um tipo de argumento de cadeia de caracteres onde o caractere de espaço `char(32)` ou outros caracteres especificados são removidos de ambos os lados. Retorna `NULL` se a cadeia de caracteres de entrada é `NULL`.

## <a name="remarks"></a>Remarks   
Por padrão `TRIM` função remove o caractere de espaço `char(32)` de ambos os lados. Isso é equivalente a `LTRIM(RTRIM(@string))`. Comportamento de `TRIM ` função com os caracteres especificados é idêntica ao comportamento de `REPLACE` função onde os caracteres do início ou término são substituídos por cadeias de caracteres vazias.


## <a name="examples"></a>Exemplos
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  Remove o caractere de espaço de ambos os lados da cadeia de caracteres   
O exemplo a seguir remove os espaços de antes e depois da palavra `test`.   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  Remove determinados caracteres de ambos os lados da cadeia de caracteres   
O exemplo a seguir remove um ponto à direita e espaços à direita.
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>Consulte também
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
