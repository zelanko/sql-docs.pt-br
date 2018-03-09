---
title: MSSQLSERVER_10520 | Microsoft Docs
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
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92ec45949632fb9c820da5979c5b119105662fdc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10520|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_PARAM_NOT_ALLOWED|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque @type foi especificado como '%ls' e um valor não NULL está especificado para o parâmetro '%ls'. Esse tipo requer um valor NULL para o parâmetro. Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.|  
  
## <a name="explanation"></a>Explicação  
O tipo especificado em @type exige um valor NULL para o parâmetro especificado; entretanto, foi fornecido um valor não NULL.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.  
  
## <a name="see-also"></a>Consulte também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
  
