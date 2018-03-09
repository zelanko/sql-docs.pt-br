---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3bad7ac89e53fb1de9c814cc64618f966e328b66
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10507|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_STMT_DOES_NOT_MATCH|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque a instrução especificada por **@stmt** e **@module_or_batch** ou por **@plan_handle** e **@statement_start_offset**, não corresponde a nenhuma instrução no módulo ou no lote especificado. Modifique os valores para que correspondam a uma instrução no módulo ou lote.|  
  
## <a name="explanation"></a>Explicação  
Uma instrução no módulo ou lote especificado não correspondeu à instrução especificada ou ao valor de deslocamento da instrução.  
  
## <a name="user-action"></a>Ação do usuário  
Modifique os valores de parâmetro especificados para que correspondam a uma instrução no módulo ou lote.  
  
## <a name="see-also"></a>Consulte também  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
