---
title: Aggregate Functions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ea34866d4a0a95b9ab3a58e2ddd720f8364f6e45
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945114"
---
# <a name="aggregate-functions-transact-sql"></a>Funções de agregação (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma função de agregação executa um cálculo em um conjunto de valores e retorna um único valor. Com exceção de `COUNT`, as funções de agregação ignoram valores nulos. As funções de agregação frequentemente são usadas com a cláusula GROUP BY da instrução SELECT.
  
Todas as funções de agregação são determinísticas. Em outras palavras, as funções de agregação retornam o mesmo valor sempre que são chamadas, quando chamadas com um conjunto específico de valores de entrada. Veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para obter mais informações sobre determinismo de funções. A [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md) pode seguir todas as funções de agregação, exceto as funções STRING_AGG, GROUPING ou GROUPING_ID.
  
Use as funções de agregação como expressões apenas nas seguintes situações:
-   A lista de seleção de uma instrução SELECT (uma subconsulta ou uma consulta externa).  
-   Uma cláusula HAVING.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] fornece as seguintes funções de agregação:
  
|||
|-|-|
|[APPROX_COUNT_DISTINCT](../../t-sql/functions/approx-count-distinct-transact-sql.md)| [MIN](../../t-sql/functions/min-transact-sql.md)|
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|
|[COUNT](../../t-sql/functions/count-transact-sql.md)|[STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)|
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[SUM](../../t-sql/functions/sum-transact-sql.md)|
|[GROUPING](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|
|[MAX](../../t-sql/functions/max-transact-sql.md)||
  
## <a name="see-also"></a>Confira também
[Funções internas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
