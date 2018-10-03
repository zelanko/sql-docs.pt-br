---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 419b45c688f755d6e5f7cf86154ce6cc527fc6ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761654"
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
