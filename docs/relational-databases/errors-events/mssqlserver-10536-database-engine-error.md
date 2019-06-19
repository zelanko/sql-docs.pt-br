---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c5e9c4574c462ef42b0235e843970c882532dc56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048987"
---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
