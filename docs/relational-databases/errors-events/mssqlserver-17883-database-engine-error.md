---
title: MSSQLSERVER_17883 | Microsoft Docs
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
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6228ef52269a304a5e72a3ff3bc50b915ab372f4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17883"></a>MSSQLSERVER_17883
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17883|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_SCHEDULER_NONYIELDING|  
|Texto da mensagem|Processo %ld:%ld:%ld (0x%lx) Trabalhador 0x%p parece não estar produzindo no Agendador %ld. Hora de criação do thread: % I64d. Thread aprox. de uso da CPU: kernel %I64d ms, usuário %I64d ms. Utilização do processo %d%%. Sistema inativo %d%%. Intervalo: %I64d ms.|  
  
## <a name="explanation"></a>Explicação  
Indica que há um possível problema com um thread que não está produzindo em um agendador.  Isso pode ocorrer devido a um bug no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver obtendo ciclos necessários para a execução.  Esse erro pode deixar de ocorrer caso o thread passe a ter produções eventualmente.  
  
## <a name="user-action"></a>Ação do usuário  
Em caso de carga excessiva no sistema, reduza a carga; caso contrário, entre em contato com os Serviços de Atendimento ao Cliente da Microsoft.  
  

