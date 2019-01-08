---
title: sys.dm_exec_session_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 89054576eb64a913e67bf3ae9a3f53d0c79eb48f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206605"
---
# <a name="sysdmexecsessionwaitstats-transact-sql"></a>sys.dm_exec_session_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre todas as esperas encontradas por threads executados para cada sessão. Você pode usar este modo de exibição para diagnosticar problemas de desempenho com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão e também com consultas e lotes específicos.  Essa exibição retorna as mesmas informações que são agregadas por sessão [DM os_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) , mas fornece a **session_id** número também.  
  
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|A id da sessão.|  
|wait_type|**nvarchar(60)**|Nome do tipo de espera. Para obter mais informações, confira [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|waiting_tasks_count|**bigint**|Número de esperas nesse tipo de espera. O contador é incrementado no início de cada espera.|  
|wait_time_ms|**bigint**|Tempo de espera total para esse tipo de espera em milissegundos. Essa hora é inclusiva de signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tempo de espera máximo neste tipo de espera.|  
|signal_wait_time_ms|**bigint**|Diferença entre a hora em que o thread de espera foi sinalizado e quando ele começou a ser executado.|  
  
## <a name="remarks"></a>Comentários  
 Essa DMV redefine as informações para uma sessão quando a sessão é aberta ou quando a sessão é reiniciada (se o pooling de conexão),  
  
 Para obter informações sobre os tipos de espera, consulte [DM os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Se o usuário tiver **VIEW SERVER STATE** permissão no servidor, o usuário verá todas as sessões em execução na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; caso contrário, o usuário verá apenas a sessão atual.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
