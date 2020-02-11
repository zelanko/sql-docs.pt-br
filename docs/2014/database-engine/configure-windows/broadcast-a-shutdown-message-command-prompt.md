---
title: Difundir uma mensagem de desligamento (prompt de comando) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, stopping
- named instances [SQL Server], broadcasting shutdown messages
- shutdown message broadcast
- broadcasting shutdown message
- command prompt [SQL Server], broadcasting shutdown messages
- default instances [SQL Server], broadcasting shutdown messages
- stopping SQL Server
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5349f45891dbca2c9135c38c1976f71c87491212
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62786647"
---
# <a name="broadcast-a-shutdown-message-command-prompt"></a>Difundir uma mensagem de desligamento (prompt de comando)
  Este tópico descreve como difundir uma mensagem de desligamento no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o comando **net send** . Na mensagem, inclua a hora em que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será interrompida de forma que os usuários possam terminar suas tarefas.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-broadcast-a-shutdown-message"></a>Para difundir uma mensagem de desligamento  
  
1.  Em um prompt de comando, digite:  
  
     **net send /users "mensagem"**  
  
     A opção **/users** especifica que a mensagem será enviada a todos os usuários conectados no servidor  
  
> [!NOTE]  
>  O comando **net send** exige que o serviço de mensagens seja executado nos computadores de envio e de recebimento. O serviço de mensagens é desabilitado por padrão no Windows Server 2003. Para obter informações sobre o **net send**, consulte a documentação do Windows.  
  
 Em sua rede, pode ser mais apropriado contatar os usuários por e-mail ou telefone. Para determinar quais usuários estão conectados atualmente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o Monitor de Atividade. Para obter informações sobre o Monitor de Atividade, veja [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md) e [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)  
  
  
