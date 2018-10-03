---
title: MSSQLSERVER_10537 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 945d569638db639f350630b424190e3aa38c35e5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095112"
---
# <a name="mssqlserver10537"></a>MSSQLSERVER_10537
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10537|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_DUP_ENABLED|  
|Texto da mensagem|Não é possível habilitar o guia de plano '%.*ls' porque o guia de plano habilitado '%.\*ls' contém o mesmo escopo e valor de deslocamento inicial da instrução. Desabilite o guia de plano existente antes de habilitar o guia de plano especificado.|  
  
## <a name="explanation"></a>Explicação  
 Um guia de plano existente contém o mesmo escopo e valor de deslocamento inicial que a instrução no guia de plano especificado.  
  
## <a name="user-action"></a>Ação do usuário  
 Desabilite o guia de plano existente antes de habilitar o guia de plano especificado.  
  
## <a name="see-also"></a>Consulte também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
