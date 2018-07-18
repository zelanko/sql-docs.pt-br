---
title: Aggregate Functions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: 30
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 77e9e561012d995670e20079c4048f12e476a994
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785698"
---
# <a name="aggregate-functions-transact-sql"></a>Funções de agregação (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma função de agregação executa um cálculo em um conjunto de valores e retorna um único valor. Com exceção de `COUNT`, as funções de agregação ignoram valores nulos. As funções de agregação frequentemente são usadas com a cláusula GROUP BY da instrução SELECT.
  
Todas as funções de agregação são determinísticas. Em outras palavras, as funções de agregação retornam o mesmo valor sempre que são chamadas, quando chamadas com um conjunto específico de valores de entrada. Veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para obter mais informações sobre determinismo de funções. A [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md) pode seguir todas as funções de agregação, exceto as funções GROUPING ou GROUPING_ID.
  
Use as funções de agregação como expressões apenas nas seguintes situações:
-   A lista de seleção de uma instrução SELECT (uma subconsulta ou uma consulta externa).  
-   Uma cláusula HAVING.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] fornece as seguintes funções de agregação:
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[MIN](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[SUM](../../t-sql/functions/sum-transact-sql.md)|  
|[COUNT](../../t-sql/functions/count-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|  
|[GROUPING](../../t-sql/functions/grouping-transact-sql.md)|[STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[MAX](../../t-sql/functions/max-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
  
## <a name="see-also"></a>Confira também
[Funções internas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
