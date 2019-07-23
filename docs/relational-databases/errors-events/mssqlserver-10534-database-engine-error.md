---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4f718b124bb9fa0fba37619349d2efc0a3bb643f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060662"
---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10534|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_INVALID_PARAMS|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque o valor especificado para **@params** é inválido. Especifique o valor no formato *parameter_name parameter_type* ou especifique NULL.|  
  
## <a name="explanation"></a>Explicação  
O valor especificado para **@params** é inválido.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique o valor no formato *parameter_name parameter_type* ou especifique NULL.  
  
## <a name="see-also"></a>Consulte Também  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
