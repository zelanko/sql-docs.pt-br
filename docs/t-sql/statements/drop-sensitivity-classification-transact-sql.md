---
title: DESCARTAR CLASSIFICAÇÃO DE CONFIDENCIALIDADE (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.author: giladm
author: giladmit
f1_keywords:
- DROP SENSITIVITY CLASSIFICATION
- DROP_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SENSITIVITY CLASSIFICATION statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d70e4a10601ab7c9171ddccf41a9ab9e5b2395c7
ms.sourcegitcommit: bc10ec0be5ddfc5f0bc220a9ac36c77dd6b80f1d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544309"
---
# <a name="drop-sensitivity-classification-transact-sql"></a>DESCARTAR CLASSIFICAÇÃO DE CONFIDENCIALIDADE (Transact-SQL)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

Descarta metadados de classificação de confidencialidade de uma ou mais colunas do banco de dados.

## <a name="syntax"></a>Sintaxe

```syntaxsql
DROP SENSITIVITY CLASSIFICATION FROM
    <object_name> [, ...n ]

<object_name> ::=
{
    [schema_name.]table_name.column_name
}
```  

## <a name="arguments"></a>Argumentos  

*object_name* ([schema_name.]table_name.column_name)

É o nome da coluna do banco de dados a partir da qual remover a classificação. Atualmente, há suporte apenas para a classificação da coluna.
    - *schema_name* (opcional) - é o nome do esquema ao qual a coluna classificada pertence.
    - *table_name* - é o nome da tabela à qual a coluna classificada pertence.
    - *column_name* - é o nome da coluna da qual remover a classificação.

## <a name="remarks"></a>Comentários  

- Várias classificações de objetos podem ser descartadas usando uma única instrução 'DROP SENSITIVITY CLASSIFICATION'.

## <a name="permissions"></a>Permissões  

Requer a permissão ALTERAR QUALQUER CLASSIFICAÇÃO DE CONFIDENCIALIDADE. A ALTER ANY SENSITIVITY CLASSIFICATION está implícita na permissão de banco de dados ALTER ou pelo servidor de permissão CONTROL SERVER.


## <a name="examples"></a>Exemplos  


### <a name="a-dropping-classification-from-a-single-column"></a>a. Descartar a classificação de uma única coluna

O exemplo a seguir remove a classificação da coluna `dbo.sales.price`.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price
```

### <a name="b-dropping-classification-from-multiple-columns"></a>B. Descartar a classificação de várias colunas

O exemplo a seguir remove a classificação das colunas `dbo.sales.price`, `dbo.sales.discount`, e `SalesLT.Customer.Phone`.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price, dbo.sales.discount, SalesLT.Customer.Phone  
```

## <a name="see-also"></a>Consulte Também  

[ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[Introdução à Proteção de Informações do SQL](https://aka.ms/sqlip)
