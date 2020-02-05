---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: efe1822be148cb702e83da9685be52dbee74ff13
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72006081"
---
# <a name="mssqlserver_10519"></a>MSSQLSERVER_10519
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10519|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque as dicas especificadas em **\@hints** não podem ser aplicadas à instrução especificada por **\@stmt** ou **\@statement_start_offset**. Verifique se as dicas podem ser aplicadas à instrução.|  
  
## <a name="explanation"></a>Explicação  
As dicas especificadas em **\@hints** não podem ser aplicadas à instrução especificada por **\@stmt** ou **\@statement_start_offset**.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique dicas que possam ser aplicadas à instrução.  
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
