---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 171d063e746393709629720dae40eb207d45d584
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Concatena um número variável de argumentos com um delimitador especificado no 1º argumento. (`CONCAT_WS` indica *concatenar com separador*.)

##  <a name="syntax"></a>Sintaxe   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>Argumentos   
separator  
É uma expressão de qualquer tipo de caractere (`nvarchar`, `varchar`, `nchar` ou `char`).

argument1, argument2, argument*N*  
É uma expressão de qualquer tipo.

## <a name="return-types"></a>Tipos de retorno
Cadeia de caracteres. O comprimento e o tipo dependem da entrada.

## <a name="remarks"></a>Remarks   
`CONCAT_WS` aceita um número variável de argumentos e os concatena em uma única cadeia de caracteres usando o primeiro argumento como separador. Ele requer um separador e pelo menos dois argumentos; caso contrário, será gerado um erro. Todos os argumentos são convertidos implicitamente em tipos de cadeia de caracteres e depois concatenados. 

A conversão implícita em cadeias de caracteres segue as regras existentes para conversões de tipo de dados. Para obter mais informações sobre conversões de tipo de dados e comportamento, veja [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md).

### <a name="treatment-of-null-values"></a>Tratamento de valores NULL

`CONCAT_WS` ignora a configuração `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}`.

Se todos os argumentos forem nulos, uma cadeia de caracteres vazia do tipo `varchar(1)` será retornada. 

Valores nulos são ignorados durante a concatenação e não adicionam o separador. Isso facilita o cenário comum da concatenação de cadeias de caracteres que geralmente têm valores em branco, como um segundo campo de endereço. Veja o exemplo B.

Se o seu cenário exigir que valores nulos sejam incluídos com um separador, veja o exemplo C usando a função `ISNULL`.

## <a name="examples"></a>Exemplos   

### <a name="a--concatenating-values-with-separator"></a>A.  Concatenando valores com separador
O exemplo a seguir concatena três colunas da tabela sys.databases, separando-os com um `- `.   

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
O exemplo a seguir ignora valores `NULL` na lista de argumentos.

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
O exemplo a seguir usa uma vírgula como separador e adiciona o caractere de retorno de carro para resultar no formato de valores separados por coluna.

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

CONCAT_WS ignorará valores NULL nas colunas. Se algumas das colunas forem anuláveis, encapsule-as com a função `ISNULL` e forneça o valor padrão, como no exemplo a seguir:

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

