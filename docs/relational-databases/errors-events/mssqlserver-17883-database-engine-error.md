---
description: MSSQLSERVER_17883
title: MSSQLSERVER_17883 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e6b7e4e7321277c47ccab2adf6e4431fea71e58c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456343"
---
# <a name="mssqlserver_17883"></a>MSSQLSERVER_17883
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|17883|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_SCHEDULER_NONYIELDING|  
|Texto da mensagem|Processo %ld:%ld:%ld (0x%lx) Trabalhador 0x%p parece não estar produzindo no Agendador %ld. Hora de criação do thread: % I64d. Thread aprox. de uso da CPU: kernel %I64d ms, usuário %I64d ms. Utilização do processo %d%%. Sistema inativo %d%%. Intervalo: %I64d ms.|  
  
## <a name="explanation"></a>Explicação  
Indica que há um possível problema com um thread que não está produzindo em um agendador.  Isso pode ocorrer devido a um bug no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver obtendo ciclos necessários para a execução.  Esse erro pode deixar de ocorrer caso o thread passe a ter produções eventualmente.  
  
## <a name="user-action"></a>Ação do usuário  
Em caso de carga excessiva no sistema, reduza a carga; caso contrário, entre em contato com os Serviços de Atendimento ao Cliente da Microsoft.  
  
