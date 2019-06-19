---
title: 'Atribuição de Nova Função: Editar página atribuição de função (Gerenciador de relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 3319ced0-4b86-42af-b18d-da41a625113c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9480b0729e7c08117ba5633c6934eca1903a61b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108163"
---
# <a name="new-role-assignment-edit-role-assignment-page-report-manager"></a>Atribuição de Nova Função: Editar página atribuição de função (Gerenciador de relatórios)
  Use a página Atribuição de Nova Função ou Editar Atribuição de Função para conceder permissões a itens de servidor de relatório e operações. Cada usuário que solicita acesso a um servidor de relatórios deve ter uma atribuição de função que define o nível de acesso. Você pode criar atribuições de função no nó raiz ou em determinado relatório, modelo, pasta, recurso ou fonte de dados compartilhada. A segurança do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é imposta pelas atribuições de função que você aplica aos itens. Uma atribuição de função faz a correspondência entre um grupo ou usuário e uma definição de função, sendo que cada definição identifica as tarefas que os grupos ou usuários podem executar em um item específico.  
  
 As atribuições de função no nível de item podem ter um grande impacto. Embora elas possam ser associadas a um único relatório ou pasta, também podem ser definidas em um nível mais alto na hierarquia de pastas e podem ser herdadas por pastas e itens que estão na parte inferior da árvore. Para obter mais informações, consulte [Conceder acesso ao usuário a um servidor de relatório &#40;Gerenciador de Relatórios&#41;](security/grant-user-access-to-a-report-server.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-new-role-assignment-or-edit-role-assignment-page"></a>Para abrir a página Atribuição de Nova Função ou a página Editar Atribuição de Função  
  
1.  Abra o Gerenciador de Relatórios e localize um item para o qual você deseja adicionar uma nova atribuição de função ou editar uma atribuição de função.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Segurança**. Esse procedimento abre a página de propriedades de Segurança do item.  
  
4.  Se desejar adicionar uma nova atribuição de função, na barra de ferramentas, clique em **Atribuição de Nova Função**. Se desejar editar uma atribuição de função, clique em **Editar** , ao lado do nome do grupo ou usuário a ser editado.  
  
    > [!NOTE]  
    >  Se um item atualmente herda a segurança de um item pai, clique em **Editar Segurança de Item** na barra de ferramentas para alterar as configurações de segurança.  
  
## <a name="options"></a>Opções  
 **Nome do grupo ou usuário**  
 Digite o nome de uma conta de grupo ou de usuário para a qual a atribuição de função está sendo criada. O nome do grupo ou usuário deve ser uma conta de domínio do Windows válida. Insira a conta neste formato: \<domínio >\\< conta\>.  
  
> [!NOTE]  
>  Esta caixa só está disponível na página Atribuição de Nova Função.  
  
 **Função**  
 Mostra todas as funções definidas no servidor de relatório que podem ser usadas para definir a segurança dos itens. Quando você cria ou altera uma atribuição de função para um relatório ou pasta, selecione uma ou mais funções até que o conjunto combinado de tarefas descreva as ações que o usuário deve ter permissão de executar. Para exibir o conjunto de tarefas a que cada função dá suporte, use o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Você não pode exibir, criar, modificar ou excluir funções no Gerenciador de Relatórios. Para obter instruções, consulte [criar, excluir ou modificar uma função &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md).  
  
 **Descrição**  
 Exibe informações adicionais sobre a função. Para funções predefinidas como **Navegador** ou **Gerenciador de Conteúdo**, a descrição resume as tarefas para as quais cada função dá suporte.  
  
 **Excluir atribuição de função**  
 Clique para excluir uma atribuição de função existente de um usuário ou grupo. Não será possível excluir uma atribuição de função se ela for a única que resta (cada item deve ter pelo menos uma atribuição de função).  
  
> [!NOTE]  
>  Este botão só está disponível na página Editar Atribuição de Função.  
  
## <a name="see-also"></a>Consulte também  
 [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Atribuições de função](security/role-assignments.md)   
 [Conceder acesso ao usuário a um servidor de relatório &#40;Gerenciador de Relatórios&#41;](security/grant-user-access-to-a-report-server.md)  
  
  
