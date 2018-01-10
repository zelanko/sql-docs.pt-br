---
title: "Propriedades de função do sistema (Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
caps.latest.revision: "30"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8028ef472cd23de251ab791e4099703640fdabc3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="system-role-properties-management-studio"></a>Propriedades de Função do Sistema (Management Studio)
  Use a página Funções do Sistema para exibir as definições de funções do sistema atualmente definidas no servidor de relatório. Uma definição de função do sistema contém uma coleção de tarefas nomeada executada com relação a todo o site e não com relação a um item individual. Definições de função são atribuídas a um usuário ou a grupos para criar uma atribuição de função resultante. As tarefas na definição de função especificam o que o usuário ou grupo pode fazer.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tem duas definições de função do sistema predefinidas: **Administrador do Sistema** e **Usuário do Sistema**. Você pode modificar essas definições de função alterando a lista de tarefas ou pode criar uma nova definição de função que ofereça suporte a diferentes combinações de tarefas. A edição de uma definição de função afeta todas as atribuições de função que incluem a definição da função.  
  
> [!NOTE]  
>  Atribuições de função do sistema só são usadas em um servidor de relatório executado no modo nativo. Se o servidor de relatório for configurado para integração do SharePoint, essa página não estará disponível.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica o nome da definição de função do aplicativo.  
  
 **Descrição**  
 Mostra uma descrição da definição da função no sistema. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], esta descrição só é visível nesta página. Os usuários que exibirem esse item no Gerenciador de Relatórios poderão ver essa descrição ao navegar na hierarquia de pastas.  
  
 **Tarefa**  
 Lista todas as tarefas no nível de sistema que podem ser selecionadas para essa definição de função. Você pode adicionar ou remover itens da lista de tarefas predefinidas para definir como os usuários acessam um determinado item com essa função. Você não pode criar tarefas novas nem modificar tarefas existentes.  
  
 **Descrição**  
 Fornece informações sobre cada tarefa. Você não pode modificar descrições de tarefa.  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Tarefas em nível de sistema](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)   
 [Tarefas e permissões](../../reporting-services/security/tasks-and-permissions.md)   
 [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
