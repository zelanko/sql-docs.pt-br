---
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b0f90d85d5194218a1913cbc00186111e1d4c183
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver10521"></a>MSSQLSERVER_10521
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10521|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_PARAM_NEEDED|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque **@type** foi especificado como '%ls' e o parâmetro '%ls' é NULL. Esse tipo requer um valor não NULL para o parâmetro. Especifique um valor não NULL para o parâmetro ou altere o tipo para um que permita um valor NULL para o parâmetro.|  
  
## <a name="explanation"></a>Explicação  
O tipo especificado em **@type** exige um valor não NULL para o parâmetro especificado; entretanto, foi fornecido um valor NULL.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique um valor não NULL para o parâmetro ou altere o tipo para um que permita um valor NULL para o parâmetro.  
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
