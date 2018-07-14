---
title: sys.dm_pdw_os_threads (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ddc12f05-edeb-4848-b6d7-e851684cf044
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 1009f1f5fea70e7af6a3c918d514193d997c2836
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926797"
---
# <a name="sysdmpdwosthreads-transact-sql"></a>sys.dm_pdw_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|A ID do nó afetado.<br /><br /> pdw_node_id e thread_id formam a chave para esta exibição.|Consulte node_id na [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|thread_id|**int**|pdw_node_id e thread_id formam a chave para esta exibição.||  
|process_id|**int**|||  
|nome|**nvarchar(255)**|||  
|priority|**int**|||  
|start_time|**datetime**|||  
|state|**nvarchar(32)**|||  
|wait_reason|**nvarchar(32)**|||  
|total_processor_elapsed_time|**bigint**|Tempo total do kernel usado pelo thread.||  
|total_user_elapsed_time|**bigint**|Tempo total de usuário usado pelo thread||  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
