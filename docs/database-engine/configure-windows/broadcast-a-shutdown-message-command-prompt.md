---
title: Difundir uma mensagem de desligamento (prompt de comando) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server, stopping
- named instances [SQL Server], broadcasting shutdown messages
- shutdown message broadcast
- broadcasting shutdown message
- command prompt [SQL Server], broadcasting shutdown messages
- default instances [SQL Server], broadcasting shutdown messages
- stopping SQL Server
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
caps.latest.revision: "28"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6620f8c7d0bc5bb8bd8a2b94b927e6cec8bf7468
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="broadcast-a-shutdown-message-command-prompt"></a>Difundir uma mensagem de desligamento (prompt de comando)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como difundir uma mensagem de desligamento no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o comando **net send**. Na mensagem, inclua a hora em que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será interrompida de forma que os usuários possam terminar suas tarefas.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-broadcast-a-shutdown-message"></a>Para difundir uma mensagem de desligamento  
  
1.  Em um prompt de comando, digite:  
  
     **net send /users "mensagem"**  
  
     A opção **/users** especifica que a mensagem será enviada a todos os usuários conectados no servidor  
  
> [!NOTE]  
>  O comando **net send** exige que o serviço de mensagens seja executado nos computadores de envio e de recebimento. O serviço de mensagens é desabilitado por padrão no Windows Server 2003. Para obter informações sobre o **net send**, consulte a documentação do Windows.  
  
 Em sua rede, pode ser mais apropriado contatar os usuários por e-mail ou telefone. Para determinar quais usuários estão conectados atualmente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o Monitor de Atividade. Para obter informações sobre o Monitor de Atividade, veja [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md) e [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
