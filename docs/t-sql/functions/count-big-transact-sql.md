---
title: COUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d72ac52b0b1bf5885c9ad093ebbadfa2c6919cd8
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81629433"
---
# <a name="count_big-transact-sql"></a>COUNT_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna o número de itens encontrados em um grupo. `COUNT_BIG` funciona como a função [COUNT](../../t-sql/functions/count-transact-sql.md). Essas funções são diferentes apenas nos tipos de dados de seus valores de retorno. `COUNT_BIG` sempre retorna um valor do tipo de dados **bigint**. `COUNT` sempre retorna um valor do tipo de dados **int**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( [ ALL ] { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
ALL  
Aplica a função de agregação a todos os valores. ALL funciona como o padrão.
  
DISTINTO  
Especifica que `COUNT_BIG` retorna o número de valores não nulos exclusivos.
  
*expressão*  
Uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo. `COUNT_BIG` não oferece suporte a funções de agregação ou subconsultas em uma expressão.
  
*\**  
Especifica que `COUNT_BIG` deve contar todas as linhas para determinar a contagem total de linhas da tabela para retornar. `COUNT_BIG(*)` não usa nenhum parâmetro e não oferece suporte ao uso de DISTINCT. `COUNT_BIG(*)` não exige um parâmetro *expression* porque, por definição, não usa informações sobre nenhuma coluna específica. `COUNT_BIG(*)` retorna o número de linhas em uma tabela especificada e preserva linhas duplicatas. Ele conta cada linha separadamente, inclusive as linhas que contêm valores nulos.
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
A *partition_by_clause* divide o conjunto de resultados produzido pela cláusula `FROM` em partições às quais a função `COUNT_BIG` é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. A *order_by_clause* determina a ordem lógica da operação. Veja [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md) para saber mais.
  
## <a name="return-types"></a>Tipos de retorno
**bigint**
  
## <a name="remarks"></a>Comentários  
COUNT_BIG(\*) retorna o número de itens de um grupo. Isso inclui valores NULL e duplicatas.
  
COUNT_BIG (ALL *expression*) avalia a *expression* de cada linha em um grupo e retorna o número de valores não nulos.
  
COUNT_BIG (DISTINCT *expression*) avalia a *expression* de cada linha em um grupo e retorna o número de valores não nulos exclusivos.
  
COUNT_BIG é uma função determinística quando usada **_sem_** as cláusulas OVER e ORDER BY. COUNT_BIG é não determinístico quando especificado **_com_** as cláusulas OVER e ORDER BY. Veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para saber mais.
  
## <a name="examples"></a>Exemplos  
Veja [COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md) para ter exemplos.
  
## <a name="see-also"></a>Confira também
[Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)  
[int, bigint, smallint e tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
