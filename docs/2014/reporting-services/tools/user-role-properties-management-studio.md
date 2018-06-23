---
title: Propriedades de Função de Usuário (Management Studio) | Microsoft Docs
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
- sql12.swb.reportserver.userroleproperties.f1
ms.assetid: c8b22236-a8b1-4e15-b1ff-4e1909b602d3
caps.latest.revision: 26
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 23ba8d4fc4647efc28ae65184e1477d4ad800e10
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115153"
---
# <a name="user-role-properties-management-studio"></a>Propriedades de Função do Usuário (Management Studio)
  Use essa página para exibir quais tarefas são incluídas em uma definição de função de nível de item. Essa página também pode ser usada para alterar a lista de tarefas ou modificar uma descrição de função.  
  
 Uma definição de função de nível de item é uma coleção nomeada de tarefas que os usuários executam referentes a um item específico (ou seja, uma pasta, um relatório, recurso ou fonte de dados compartilhada). Definições de função são atribuídas a um usuário ou grupo para criar uma atribuição de função no Gerenciador de Relatórios. As tarefas na definição de função descrevem o que o usuário ou grupo pode fazer.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui várias definições predefinidas de função de nível de item com as que você pode trabalhar. Você pode modificar as definições de função alterando a lista de tarefas de cada um. A edição de uma definição de função afeta todas as atribuições de função que incluem a definição da função.  
  
> [!NOTE]  
>  Atribuições de função de usuário só são usadas em um servidor de relatório que executa em modo nativo. Se o servidor de relatório estiver configurado para integração do SharePoint, essa página exibirá informações somente leitura sobre as funções e o nível de permissão definidos no site do SharePoint.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica o nome da definição de função.  
  
 **Descrição**  
 Exibe uma descrição da definição da função. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], esta descrição só é visível nesta página. No Gerenciador de Relatórios, essa descrição ajuda os usuários a decidir se a função deve ser usada em atribuição de função.  
  
 **Tarefa**  
 Lista todas as tarefas de nível de item que podem ser selecionadas para essa definição de função. Você pode adicionar ou remover itens da lista de tarefas predefinidas para definir como os usuários acessam um determinado item com essa função. Você não pode criar tarefas novas nem modificar tarefas existentes. A lista de tarefas de uma definição de função só aparece no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Descrição da tarefa**  
 Fornece informações sobre cada tarefa. Você não pode modificar descrições de tarefa.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas em nível de item](../security/tasks-and-permissions-item-level-tasks.md)   
 [Definições de função](../security/role-definitions.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Tarefas e permissões](../security/tasks-and-permissions.md)   
 [Funções predefinidas](../security/role-definitions-predefined-roles.md)  
  
  