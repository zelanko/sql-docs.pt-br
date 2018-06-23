---
title: Tarefas em nível do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: de33e7370e141e07ac61b6e62d6d1d0cc44ffdc4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117332"
---
# <a name="system-level-tasks"></a>Tarefas de nível de sistema
  Uma tarefa em nível do sistema é uma coleção de permissões relacionadas a operações que se aplicam ao site do servidor de relatório como um todo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também inclui tarefas em nível de item que se aplicam a itens específicos. Para obter mais informações, consulte [Tarefas em nível de item](tasks-and-permissions-item-level-tasks.md). Para obter mais informações sobre as tarefas e permissões em geral, consulte [tarefas e permissões](tasks-and-permissions.md).  
  
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
 [Conceder permissões em um servidor de relatório no Modo Nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  