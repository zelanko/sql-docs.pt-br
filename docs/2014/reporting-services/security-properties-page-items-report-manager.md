---
title: Página de propriedades de segurança, itens (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 351b8503-354f-4b1b-a7ac-f1245d978da0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 87bdd8c30468f18a30de5bcb3ee122469ac3958c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189606"
---
# <a name="security-properties-page-items-report-manager"></a>Página Propriedades de Segurança, Itens (Gerenciador de Relatórios)
  Use a página Propriedades de Segurança para exibir ou modificar as definições de segurança que determinam acesso a pastas, relatórios, modelos, recursos e fontes de dados compartilhadas. Essa página está disponível para itens que você tem permissão para proteger.  
  
 O acesso aos itens é definido por atribuições de função que especificam as tarefas que um grupo ou usuário podem executar. Uma atribuição de função consiste em um nome de usuário ou grupo e em uma ou mais definições de função que especificam uma coleção de tarefas.  
  
 As configurações de segurança são herdadas da pasta raiz até subpastas e itens dentro dessas pastas. A menos que você interrompa explicitamente a segurança herdada, subpastas e itens herdam o contexto de segurança de um item pai. Se você redefinir política de segurança para uma pasta no meio da hierarquia, todos os itens filhos, incluindo subpastas, assumirão as novas definições de segurança.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-security-page-for-an-item"></a>Para abrir a página Segurança de um item  
  
1.  Abra o Gerenciador de Relatórios e localize o item cujas configurações de segurança você deseja definir.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, execute uma destas etapas:  
  
    -   Clique em **Segurança**. Esse procedimento abre a página de propriedades de Segurança do item.  
  
    -   Clique em **Gerenciar** para abrir a página Propriedades Gerais do item. Em seguida, selecione a guia **Segurança** .  
  
 **Editar Segurança de Item**  
 Clique para alterar a maneira como a segurança é definida para o item atual. Se você estiver editando segurança para uma pasta, suas alterações se aplicarão ao conteúdo da pasta atual e de quaisquer subpastas.  
  
 Esse botão não está disponível para a pasta Base.  
  
 Os botões a seguir ficam disponíveis quando você edita segurança de item.  
  
 **Delete (excluir)**  
 Marque a caixa de seleção próximo ao grupo ou nome de usuário que você quer excluir e clique em **Excluir**. Você não pode excluir uma atribuição de função se ela for a única ou se for uma atribuição de função interna (por exemplo, "Built-in\Administrators") que define os parâmetros de segurança do servidor de relatório. A exclusão de uma atribuição de função não exclui uma conta de grupo ou usuário, nem as definições da função.  
  
 **Nova atribuição de função**  
 Clique para abrir a página Atribuição de Nova Função que é usada para criar atribuições de função adicionais para o item atual. Para obter mais informações, consulte [nova atribuição de função: Editar página de atribuição de função &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/new-role-assignment-edit-role-assignment-page-report-manager.md).  
  
 **Reverter em segurança pai**  
 Clique para redefinir as configurações de segurança às da pasta pai imediata. Se a segurança não puder ser quebrada na hierarquia de pastas do servidor de relatórios, as configurações de segurança na pasta de alto nível, Base, serão usadas.  
  
 **Grupo ou usuário**  
 Lista os grupos e usuários que fazem parte de uma atribuição de função existente para o item atual. Atribuições de função existentes para a pasta atual são definidas para os grupos e usuários que aparecem nesta coluna. Você pode clicar em um grupo ou nome de usuário para exibir ou editar detalhes da atribuição de função.  
  
 **Roles**  
 Lista uma ou mais definições de função que fazem parte de uma atribuição de função existente. Se várias funções forem atribuídas a um grupo ou conta de usuário, aquele grupo de usuários pode desempenhar todas as tarefas que pertencem àquelas funções. Para exibir as tarefas associadas a uma função, use o SQL Server Management Studio para exibir as tarefas de cada definição de função.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Funções predefinidas](security/role-definitions-predefined-roles.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Atribuições de função](security/role-assignments.md)   
 [Definições de função](security/role-definitions.md)  
  
  
