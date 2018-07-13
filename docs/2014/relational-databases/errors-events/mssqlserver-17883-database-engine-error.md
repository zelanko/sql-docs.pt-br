---
title: MSSQLSERVER_17883 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 83b09894887f861fd29abf7722ba4166d28d81bf
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411375"
---
# <a name="mssqlserver17883"></a>MSSQLSERVER_17883
    
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
  
  
