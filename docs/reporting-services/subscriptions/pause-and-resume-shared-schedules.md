---
title: Pausar e retomar agendas compartilhadas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pausing schedules
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services], resuming
- resuming schedules
- continuing schedules
- schedules [Reporting Services], resuming
- schedules [Reporting Services], pausing
ms.assetid: e416be75-5234-4aa6-a3de-77f60f25169a
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0eceb425b1294026a1c82043800c6aaa2ec83972
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="pause-and-resume-shared-schedules"></a>Pausar e retomar agendas compartilhadas
  Você pode pausar e retomar uma agenda compartilhada em uso. Pausar uma agenda compartilhada é uma maneira de congelar temporariamente uma agenda usada para disparar o processamento de relatórios e assinaturas. Somente agendas compartilhadas podem ser pausadas e reiniciadas. Não é possível pausar agendas específicas a relatórios.  
  
 Não é possível pausar e retomar o processamento de um relatório em andamento. Você só pode pausar e retomar agendamentos que estejam na fila de agendamento do serviço SQL Server Agent. Um trabalho em andamento está fora do escopo do mecanismo de agendamento. Para obter mais informações, consulte [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
 Enquanto uma agenda compartilhada estiver pausada, todas as operações que teriam ocorrido são ignoradas. Ao permitir que uma agenda compartilhada continue, o processamento de relatórios e assinaturas ocorrerá no próximo horário agendado, usando o horário local do servidor. O servidor de relatórios do modo nativo ou aplicativos de serviço do SharePoint não compensa pelas operações agendadas que teriam ocorrido se o agendamento não tivesse sido pausado.  
  
 Neste tópico:  
  
-   [Pausar e retomar agendas compartilhadas (modo Nativo)](#bkmk_native)  
  
-   [Pausar e retomar agendas compartilhadas (modo SharePoint)](#bkmk_sharepoint)  
  
##  <a name="bkmk_native"></a> Pausar e retomar agendas compartilhadas (modo Nativo)  
 Para pausar e retomar uma agenda compartilhada, use a página Agendas no Gerenciador de Relatórios. Não é possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]; ele não oferece opções para pausar e retomar agendas. Para obter mais informações, consulte [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md).  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>Para pausar ou retomar uma agenda compartilhada  
  
1.  No Gerenciador de Relatórios, clique em **Configurações do Site**.  
  
2.  Clique em **Agendas**.  
  
3.  Selecione a agenda e clique em **Pausar** ou em **Retomar** na faixa de opções. Se uma Agenda estiver pausada, a coluna **Status** conterá **Pausada**.  
  
##  <a name="bkmk_sharepoint"></a> Pausar e retomar agendas compartilhadas (modo SharePoint)  
 Para pausar e retomar uma agenda compartilhada, use a página Configurações do Site ou o PowerShell. As agendas são gerenciadas por site do SharePoint.  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>Para pausar ou retomar uma agenda compartilhada  
  
1.  Clique em **Ações do Site**.  
  
2.  Clique em **Configurações de Site**.  
  
3.  Na seção Reporting Services, clique em **Gerenciar Agendas Compartilhadas**.  
  
4.  Selecione a agenda e clique em **Pausar Agendas Selecionadas** ou **Executar Agendas Selecionadas**. Se uma Agenda estiver pausada, a coluna **Status** conterá **Pausada**.  
  
## <a name="see-also"></a>Consulte também  
 [Agendas](../../reporting-services/subscriptions/schedules.md)   
 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [Alterar configurações de fuso horário e relógio em um servidor de relatório](../../reporting-services/subscriptions/change-time-zones-and-clock-settings-on-a-report-server.md)   
 [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
