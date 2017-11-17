---
title: "Agregar funções (Transact-SQL) | Microsoft Docs"
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
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a97d68c641d2a3deb1d3fd3a674f65cafc3854c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions-transact-sql"></a>Funções de agregação (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

As funções de agregação executam um cálculo em um conjunto de valores e retornam um único valor. Com exceção de COUNT, as funções de agregação ignoram valores nulos. As funções de agregação normalmente são usadas com a cláusula GROUP BY da instrução SELECT.
  
Todas as funções de agregação são determinísticas. Isso significa que as funções de agregação retornam o mesmo valor sempre que são chamadas com o uso de um conjunto específico de valores de entrada. Para obter mais informações sobre determinismo de função, consulte [determinísticas e funções não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). O [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md) pode seguir todas as funções de agregação exceto GROUPING e GROUPING_ID.
  
As funções de agregação podem ser usadas como expressões apenas no seguinte:
-   A lista de seleção de uma instrução SELECT (uma subconsulta ou uma consulta externa).  
-   Uma cláusula HAVING.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] fornece as seguintes funções de agregação:
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[MIN](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[SOMA](../../t-sql/functions/sum-transact-sql.md)|  
|[CONTAGEM](../../t-sql/functions/count-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|  
|[AGRUPAMENTO](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
|[MÁX.](../../t-sql/functions/max-transact-sql.md)||  
  
## <a name="see-also"></a>Consulte também
[Funções internas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[SOBRE cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

