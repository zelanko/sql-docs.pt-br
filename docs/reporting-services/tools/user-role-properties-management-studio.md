---
title: "Propriedades de Função de Usuário (Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.userroleproperties.f1
ms.assetid: c8b22236-a8b1-4e15-b1ff-4e1909b602d3
caps.latest.revision: 27
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 76bd80e1fc470d9cdb998d23834d0a3473d411fe
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="user-role-properties-management-studio"></a>Propriedades de Função do Usuário (Management Studio)
  Use essa página para exibir quais tarefas são incluídas em uma definição de função de nível de item. Essa página também pode ser usada para alterar a lista de tarefas ou modificar uma descrição de função.  
  
 Uma definição de função de nível de item é uma coleção nomeada de tarefas que os usuários executam referentes a um item específico (ou seja, uma pasta, um relatório, recurso ou fonte de dados compartilhada). Definições de função são atribuídas a um usuário ou grupo para criar uma atribuição de função no Gerenciador de Relatórios. As tarefas na definição de função descrevem o que o usuário ou grupo pode fazer.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]inclui um número de definições de função de nível de item predefinidas que você pode trabalhar com. Você pode modificar as definições de função alterando a lista de tarefas de cada um. A edição de uma definição de função afeta todas as atribuições de função que incluem a definição da função.  
  
> [!NOTE]  
>  Atribuições de função de usuário só são usadas em um servidor de relatório que executa em modo nativo. Se o servidor de relatório estiver configurado para integração do SharePoint, essa página exibirá informações somente leitura sobre as funções e o nível de permissão definidos no site do SharePoint.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica o nome da definição de função.  
  
 **Description**  
 Exibe uma descrição da definição da função. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], esta descrição só é visível nesta página. No Gerenciador de Relatórios, essa descrição ajuda os usuários a decidir se a função deve ser usada em atribuição de função.  
  
 **Tarefa**  
 Lista todas as tarefas de nível de item que podem ser selecionadas para essa definição de função. Você pode adicionar ou remover itens da lista de tarefas predefinidas para definir como os usuários acessam um determinado item com essa função. Você não pode criar tarefas novas nem modificar tarefas existentes. A lista de tarefas de uma definição de função só aparece no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Descrição da tarefa**  
 Fornece informações sobre cada tarefa. Você não pode modificar descrições de tarefa.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de nível de item](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md)   
 [Definições de função](../../reporting-services/security/role-definitions.md)   
 [Servidor de relatório na Ajuda de F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Tarefas e permissões](../../reporting-services/security/tasks-and-permissions.md)   
 [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  

