---
title: COUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_BIG_TSQL
- COUNT_BIG
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT_BIG function
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT_BIG function
ms.assetid: f2e3601f-487e-4917-bb01-47b1047908cd
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ce3046c36b7d224f6294948029cef6cf5afd43c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="countbig-transact-sql"></a>COUNT_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o número de itens de um grupo. COUNT_BIG funciona como a função COUNT. A única diferença entre as duas funções são seus valores de retorno. COUNT_BIG sempre retorna um **bigint** valor de tipo de dados. COUNT sempre retorna um **int** valor de tipo de dados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT_BIG ( { [ ALL | DISTINCT ] expression } | * )  
   [ OVER ( [ partition_by_clause ] [ order_by_clause ] ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
ALL  
Aplica a função de agregação a todos os valores. ALL é o padrão.
  
DISTINCT  
Especifica que COUNT_BIG retorna o número de valores não nulos exclusivos.
  
*expressão*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo. Funções de agregação e subconsultas não são permitidas.
  
*\**  
Especifica que todas as linhas devem ser contadas para retornar o número total de linhas em uma tabela. COUNT_BIG (*\**) não usa nenhum parâmetro e não pode ser usado com DISTINCT. COUNT_BIG (*\**) não requer um *expressão* parâmetro porque, por definição, ele não usa informações sobre nenhuma coluna específica. COUNT_BIG (*\**) retorna o número de linhas em uma tabela especificada sem descartar duplicatas. Ele conta cada linha separadamente. Isso inclui linhas que contêm valores nulos.
  
ALL  
Aplica a função de agregação a todos os valores. ALL é o padrão.
  
DISTINCT  
Especifica que AVG será executado apenas uma vez em cada instância exclusiva de um valor, por mais que esse valor ocorra.
  
*expressão*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de exato dados numéricos aproximados ou categoria de tipo, exceto para o **bit** tipo de dados. Funções de agregação e subconsultas não são permitidas.
  
SOBRE **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições para o qual a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. *order_by_clause* determina a ordem lógica na qual a operação é executada. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
**bigint**
  
## <a name="remarks"></a>Comentários  
COUNT_BIG(*) retorna o número de itens de um grupo. Isso inclui valores NULL e duplicatas.
  
COUNT_BIG (todos os *expressão*) avalia *expressão* para cada linha em um grupo e retorna o número de valores não nulos.
  
COUNT_BIG (DISTINCT *expressão*) avalia *expressão* para cada linha em um grupo e retorna o número de valores não nulos exclusivos.
  
COUNT_BIG é uma função determinística quando usada sem as cláusulas OVER e ORDER BY. É não determinística quando especificada com as cláusulas OVER e ORDER BY. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Exemplos  
Para obter exemplos, consulte [contagem &#40; Transact-SQL &#41; ](../../t-sql/functions/count-transact-sql.md).
  
## <a name="see-also"></a>Consulte também
[Funções de agregação &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[Contagem de &#40; Transact-SQL &#41;](../../t-sql/functions/count-transact-sql.md)  
[int, bigint, smallint, tinyint e #40; Transact-SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[SOBRE cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

