---
title: Propriedades de função do sistema (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3d19b145daaf3e599e96e6b4b02fac179b27e028
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019607"
---
# <a name="system-role-properties-management-studio"></a>Propriedades de Função do Sistema (Management Studio)
  Use a página Funções do Sistema para exibir as definições de funções do sistema atualmente definidas no servidor de relatório. Uma definição de função do sistema contém uma coleção de tarefas nomeada executada com relação a todo o site e não com relação a um item individual. Definições de função são atribuídas a um usuário ou a grupos para criar uma atribuição de função resultante. As tarefas na definição de função especificam o que o usuário ou grupo pode fazer.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tem duas definições de função do sistema predefinidas: **Administrador do sistema** e **usuário do sistema**. Você pode modificar essas definições de função alterando a lista de tarefas ou pode criar uma nova definição de função que ofereça suporte a diferentes combinações de tarefas. A edição de uma definição de função afeta todas as atribuições de função que incluem a definição da função.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Tarefas de nível de sistema](../security/tasks-and-permissions-system-level-tasks.md)   
 [Tarefas e permissões](../security/tasks-and-permissions.md)   
 [Funções predefinidas](../security/role-definitions-predefined-roles.md)  
  
  
