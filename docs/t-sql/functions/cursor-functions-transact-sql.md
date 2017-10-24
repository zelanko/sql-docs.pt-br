---
title: "Funções de cursor (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7cbeb217f4803da10e52e62074dbd42821b1e21
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="cursor-functions-transact-sql"></a>funções de cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

As seguintes funções escalares retornam informações sobre cursores:
  
|||  
|-|-|  
|[@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)|[CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)|  
|[@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)||  
  
Todas as funções de cursor são não determinísticas. Isso significa que essas funções nem sempre retornam os mesmos resultados a cada chamada, mesmo com o mesmo conjunto de valores de entrada. Para obter mais informações sobre determinismo de função, consulte [determinísticas e funções não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="see-also"></a>Consulte também
[Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)
  
  

