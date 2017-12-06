---
title: "Tarefas em nível do sistema | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
caps.latest.revision: "36"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fcfb30e90a7e5e387b6a7e244a842a41c8ce7012
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="tasks-and-permissions---system-level-tasks"></a>Tarefas e permissões – tarefas em nível do sistema
  Uma tarefa em nível do sistema é uma coleção de permissões relacionadas a operações que se aplicam ao site do servidor de relatório como um todo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também inclui tarefas em nível de item que se aplicam a itens específicos. Para obter mais informações, consulte [Tarefas em nível de item](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md). Para obter mais informações sobre tarefas e permissões em geral, consulte [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
> [!NOTE]  
>  Se você estiver trabalhando programaticamente com essas tarefas, deve usar métodos ofereçam suporte a tarefas de nível de sistema. Para obter mais informações, consulte <xref:ReportService2010.ReportingService2010.ListTasks%2A> e <xref:ReportService2010.ReportingService2010.ListRoles%2A>.  
  
## <a name="permissions-in-system-level-tasks"></a>Permissões em tarefas de nível de sistema  
 A tabela a seguir identifica a coleção de permissões de cada tarefa de sistema. As permissões são listadas somente para fins informativos, para fornecer uma descrição mais precisa da funcionalidade disponível em cada tarefa.  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Executar definições de relatório|Executar Definições de Relatório (o nome da permissão e da tarefa são iguais)|  
|Gerar eventos|Gerar eventos|  
|Gerenciar trabalhos|Ler Propriedades do Sistema<br /><br /> Atualizar Propriedades do Sistema|  
|Gerenciar propriedades de servidor de relatório|Ler Propriedades do Sistema<br /><br /> Atualizar Propriedades do Sistema|  
|Gerenciar funções|Criar Funções<br /><br /> Excluir Funções<br /><br /> Ler Propriedades de Função<br /><br /> Atualizar Propriedades de Função|  
|Gerenciar agendas compartilhadas|Criar Agendas|  
|Gerenciar segurança de servidor de relatório|Ler Políticas de Segurança do Sistema<br /><br /> Atualizar Políticas de Segurança do Sistema|  
|Exibir propriedades do servidor de relatório|Ler Propriedades do Sistema|  
|Exibir agendas compartilhadas|Ler Agendas|  
  
## <a name="see-also"></a>Consulte também  
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
