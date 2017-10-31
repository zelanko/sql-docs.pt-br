---
title: MSSQLSERVER_10536 | Microsoft Docs
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
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b00f374672490cf9823a3c7700d4ae0e53e18c3f
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10536|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_TOO_MANY_STMTS|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque o lote ou o módulo correspondente ao **@plan_handle** especificado contém mais de 1.000 instruções qualificadas. Crie um guia de plano para cada instrução do lote ou do módulo especificando um valor **statement_start_offset** para cada instrução.|  
  
## <a name="explanation"></a>Explicação  
O lote ou o módulo correspondente ao **@plan_handle** especificado contém mais de 1.000 instruções qualificadas.  
  
## <a name="user-action"></a>Ação do usuário  
Crie um guia de plano para cada instrução do lote ou do módulo especificando um valor **statement_start_offset** para cada instrução.  
  
## <a name="see-also"></a>Consulte também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

