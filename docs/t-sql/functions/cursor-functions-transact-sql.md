---
title: Funções de cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9c3919edabc5d0a642571f833680747a4b8bb3cc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "33988327"
---
# <a name="cursor-functions-transact-sql"></a>funções de cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Estas funções escalares retornam informações sobre cursores:
  
|||  
|-|-|  
|[@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)|[CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)|  
|[@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)||  
  
Todas as funções de cursor são não determinísticas. Em outras palavras, essas funções nem sempre retornam os mesmos resultados sempre que são executadas, mesmo com o mesmo conjunto de valores de entrada. Veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para obter mais informações sobre determinismo de funções.
  
## <a name="see-also"></a>Confira também
[Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)
  
  
