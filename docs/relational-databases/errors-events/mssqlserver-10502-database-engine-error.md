---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90c5faca34bbc936ccc71f703cadb81609bb8a90
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver10502"></a>MSSQLSERVER_10502
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10502|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_DUP_FOUND|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque a instrução especificada por @stmt e @module_or_batch ou por @plan_handle e @statement_start_offset, corresponde ao guia de plano '%.\*ls' existente no banco de dados. Descarte o guia de plano existente antes de criar o novo.|  
  
## <a name="explanation"></a>Explicação  
Há um guia de plano relativo à instrução especificada.  
  
## <a name="user-action"></a>Ação do usuário  
Descarte o guia de plano existente antes de criar o novo.  
  
## <a name="see-also"></a>Consulte Também  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
