---
title: MSSQLSERVER_10532 | Microsoft Docs
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
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e105f17279de3903519435fdc4590431ea716158
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10532"></a>MSSQLSERVER_10532
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10532|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque o lote ou o módulo especificado por **@plan_handle** não contém uma instrução qualificada para um guia de plano. Especifique outro valor para **@plan_handle**.|  
  
## <a name="explanation"></a>Explicação  
O lote ou o módulo especificado por **@plan_handle** não contém uma instrução qualificada para um guia de plano.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique outro valor para **@plan_handle**.  
  
## <a name="see-also"></a>Consulte também  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

