---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 377db445118e55f1bdeec220f1e6701e9f89706c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Concatena um número variável de argumentos com um delimitador especificado no argumento 1º. (`CONCAT_WS` indica *concatenar com separador*.)

##  <a name="syntax"></a>Sintaxe   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>Argumentos   
separador  
É uma expressão de qualquer tipo de caractere (`nvarchar`, `varchar`, `nchar`, ou `char`).

argument1 argument2, argumento*N*  
É uma expressão de qualquer tipo.

## <a name="return-types"></a>Tipos de retorno
Cadeia de caracteres. O comprimento e tipo dependem da entrada.

## <a name="remarks"></a>Comentários   
`CONCAT_WS`aceita um número variável de argumentos e os concatena em uma única cadeia de caracteres usando o primeiro argumento como separador. Ele requer um separador e um mínimo de dois argumentos; Caso contrário, ocorrerá um erro. Todos os argumentos são implicitamente convertidos em tipos de cadeia de caracteres e, em seguida, são concatenados. 

A conversão implícita em cadeias de caracteres segue as regras existentes para conversões de tipo de dados. Para obter mais informações sobre conversões de tipo de dados e comportamento, consulte [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md).

### <a name="treatment-of-null-values"></a>Tratamento de valores nulos

`CONCAT_WS`ignora o `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` configuração.

Se todos os argumentos são null, uma cadeia de caracteres vazia do tipo `varchar(1)` é retornado. 

Valores nulos são ignorados durante a concatenação e não adiciona o separador. Isso facilita o cenário comum da concatenação de cadeias de caracteres que geralmente têm valores em branco, como um segundo campo de endereço. Consulte o exemplo B.

Se seu cenário exigir valores nulos sejam incluídos com um separador, consulte o exemplo C usando o `ISNULL` função.

## <a name="examples"></a>Exemplos   

### <a name="a--concatenating-values-with-separator"></a>A.  Concatenar valores com separador
O exemplo a seguir concatena três colunas da tabela sys. Databases, separando-os com um `- `.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLES - NENHUM |
|2 - SIMPLES - NENHUM |
|3 - COMPLETO - NENHUM |
|4 - SIMPLES - NENHUM |


### <a name="b--skipping-null-values"></a>B.  Ignorar valores nulos
O exemplo a seguir ignora `NULL` valores na lista de argumentos.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  Gerando arquivo CSV de tabela
O exemplo a seguir usa uma vírgula como separador e adiciona o caractere de retorno de carro para resultar no formato de valores separados de coluna.

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

CONCAT_WS irá ignorar valores nulos nas colunas. Se algumas das colunas são nulas, colocá-los com `ISNULL` de função e fornecer o valor padrão, como no exemplo a seguir:

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>Consulte também
[Funções de cadeia de caracteres (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)      


