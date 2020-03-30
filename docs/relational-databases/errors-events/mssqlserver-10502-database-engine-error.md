---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33bb9c3e6bc3e3f1d198be344832451eafe9b22c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68095667"
---
# <a name="mssqlserver_10502"></a>MSSQLSERVER_10502
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10502|  
|Origem do Evento|MSSQLSERVER|  
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
  
