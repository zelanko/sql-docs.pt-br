---
title: MSrepl_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSrepl_transactions_TSQL
- MSrepl_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_transactions system table
ms.assetid: d325288d-47ae-4488-8799-122f7ab43459
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41593686ab853d8b285e47900535e25a111a7ea4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="msrepltransactions-transact-sql"></a>MSrepl_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSrepl_transactions** tabela contém uma linha para cada transação replicada. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**Int**|A ID do banco de dados Publicador.|  
|**xact_id**|**varbinary(16)**|A ID da transação.|  
|**xact_seqno**|**varbinary(16)**|O número de sequência da transação.|  
|**entry_time**|**datetime**|A hora em que a transação foi inserida no banco de dados de distribuição.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
