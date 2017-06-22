---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f4a15b91d34353e7bf7206b1367620e2de00ff9d
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10509|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_INVALID_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque a instrução especificada por **@stmt** ou **@statement_start_offset** contém um erro de sintaxe ou não está qualificada para uso em um guia de plano. Especifique uma única instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida ou uma posição inicial válida da instrução no lote. Para obter uma posição inicial válida, consulte a coluna statement_start_offset na função de gerenciamento dinâmico sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicação  
A instrução especificada por **@stmt** ou **@statement_start_offset** contém um erro de sintaxe ou não está qualificada para uso em um guia de plano.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique uma única instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida ou uma posição inicial válida da instrução no lote. Para obter uma posição inicial válida, consulte a coluna statement_start_offset na função de gerenciamento dinâmico sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Consulte também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

