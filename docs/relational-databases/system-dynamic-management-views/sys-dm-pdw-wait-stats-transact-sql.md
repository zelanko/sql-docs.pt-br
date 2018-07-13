---
title: sys.dm_pdw_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 52a9b00f7c2bda0b0bd488e94d1674019b9fc5cb
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36806681"
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>sys.dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações relacionadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relacionados ao estado do sistema operacional para instâncias em execução em nós diferentes. Para obter uma lista dos tipos de esperas e suas descrições, consulte [DM os_wait_stats](http://msdn.microsoft.com/en-us/library/ms179984\(v=sql.120\).aspx).  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|ID do nó que essa entrada se refere.||  
|**wait_name**|**nvarchar(255)**|Nome do tipo de espera.||  
|**max_wait_time**|**bigint**|Tempo de espera máximo desse tipo de espera.||  
|**request_count**|**bigint**|Número de esperas isso espere tipo pendente.||  
|**signal_time**|**bigint**|Diferença entre a hora em que o thread de espera foi sinalizado e quando ele começou a ser executado.||  
|**completed_count**|**bigint**|Número total de esperas desse tipo concluídas desde o último servidor reiniciar.||  
|**wait_time**|**bigint**|Tempo de espera total para esse tipo de espera em millisecons. Inclusivo de signal_time.||  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
