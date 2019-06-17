---
title: Funções analíticas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 60fbff84-673b-48ea-9254-6ecdad20e7fe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ebf74ab07a424612967f1482402928fc134d9e03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65945170"
---
# <a name="analytic-functions-transact-sql"></a>Funções analíticas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

O SQL Server é compatível com estas funções analíticas:
  
|||  
|-|-|  
|[CUME_DIST &#40;Transact-SQL&#41;](../../t-sql/functions/cume-dist-transact-sql.md)|[LEAD &#40;Transact-SQL&#41;](../../t-sql/functions/lead-transact-sql.md)|  
|[FIRST_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/first-value-transact-sql.md)|[PERCENTILE_CONT &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)|  
|[LAG &#40;Transact-SQL&#41;](../../t-sql/functions/lag-transact-sql.md)|[PERCENTILE_DISC &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-disc-transact-sql.md)|  
|[LAST_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/last-value-transact-sql.md)|[PERCENT_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)|  
  
As funções analíticas computam um valor agregado com base em um grupo de linhas. Ao contrário das funções de agregação, no entanto, as funções analíticas podem retornar várias linhas para cada grupo. Use funções analíticas para calcular médias móveis, totais acumulados, percentuais ou os primeiros N resultados de um grupo.
 
## <a name="see-also"></a>Confira também
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
