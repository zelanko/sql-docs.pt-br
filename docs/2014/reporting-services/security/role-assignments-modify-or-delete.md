---
title: Modificar ou excluir uma atribuição de função (Gerenciador de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6a562c7b9a888f6bfbb071e3068a3c4cf661c3ea
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215526"
---
# <a name="modify-or-delete-a-role-assignment-report-manager"></a>Modificar ou excluir uma atribuição de função (Gerenciador de Relatórios)
  Uma atribuição de função mapeia uma conta de grupo ou usuário para uma definição de função predefinida que inclui as tarefas que podem ser executadas. Ela determina os tipos de operações que um usuário pode executar com relação a uma pasta, relatório, modelo ou outro tipo de conteúdo. Para criar, modificar ou excluir atribuições de função, use o Gerenciador de Relatórios. Após criar uma atribuição de função para um determinado usuário ou grupo, você pode modificá-la posteriormente selecionando uma função diferente. Para revogar permissões em um servidor de relatório, exclua uma atribuição de função desse servidor.  
  
 Dependendo de seu objetivo, abordagens alternativas podem ser mais apropriadas. Os exemplos incluem a personalização ou a criação de uma nova definição de função ou a modificação da associação de uma conta de grupo no Active Directory.  
  
 Por exemplo, suponha que você tenha um grupo de usuários que precisa gerenciar todo o conteúdo, mas não deve ter o conjunto completo de permissões associadas ao Gerenciador de Conteúdo. Nesse caso, você poderia criar uma nova definição de função chamada Gerenciador de Conteúdo do Departamento que inclui todas as tarefas do Gerenciador de Conteúdo, exceto **Definir políticas de segurança para itens**.  
  
 Similarmente, se você for um administrador de sistema ou rede e for mais fácil gerenciar as contas de grupo do Active Directory do que as atribuições de função do Gerenciador de Relatórios, reduza a sobrecarga do gerenciamento das atribuições de função criando uma única atribuição de função para uma conta de grupo e, em seguida, ajuste a associação do grupo quando os usuários não precisarem mais acessar os relatórios.  
  
 Se você considerar a modificação ou a exclusão de uma atribuição de função como a melhor abordagem, verifique as atribuições de função de sistema e de item. Cada tipo de atribuição de função é configurado em páginas diferentes do Gerenciador de Relatórios.  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>Para modificar ou excluir uma atribuição de função de sistema  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  Clique em **Configurações de Site**.  
  
3.  Clique em **Segurança**. Todas as atribuições de função do nível de sistema definidas atualmente para a implantação de servidor ou de expansão são listadas pelo nome de conta.  
  
4.  Localize a atribuição de função que deseja modificar ou excluir.  
  
5.  Para adicionar ou remover a função para um usuário ou grupo específico, clique em **Editar**.  
  
6.  Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e clique em **Excluir**.  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>Para modificar ou excluir uma atribuição de função de item  
  
1.  Inicie o **Gerenciador de Relatórios** e localize o item para o qual você deseja editar ou excluir uma atribuição de função.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Segurança**.  
  
4.  Localize a atribuição de função que deseja modificar ou excluir.  
  
5.  Para adicionar ou remover a função para um usuário ou grupo específico, clique em **Editar**.  
  
6.  Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 (criar-e-gerenciar-função-assignments.md)   
 [Atribuições de função](role-assignments.md)   
 [Página Configurações do Site &#40;Gerenciador de Relatórios&#41;](../site-settings-page-report-manager.md)   
 [Atribuições de nova função do sistema: página Editar Atribuições de Função do Sistema &#40;Gerenciador de Relatórios&#41;](../new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)  
  
  
