---
title: Propriedades de função do sistema (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 1dce716a55830afa2d7e3bc38d87d9ea407ce95c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019052"
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
  
## <a name="see-also"></a>Consulte também  
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Tarefas em nível de sistema](../security/tasks-and-permissions-system-level-tasks.md)   
 [Tarefas e permissões](../security/tasks-and-permissions.md)   
 [Funções predefinidas](../security/role-definitions-predefined-roles.md)  
  
  