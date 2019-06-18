---
title: Modificar ou excluir uma atribuição de função (portal da Web do SSRS) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 28695a4849b29c6e593f42489fc149efd9a8db53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570643"
---
# <a name="role-assignments---modify-or-delete"></a>Atribuições de função – Modificar ou excluir

Uma atribuição de função mapeia uma conta de grupo ou usuário para uma função predefinida que define as tarefas que podem ser executadas. Ela determina os tipos de tarefas que um usuário executa na pasta, relatório, modelo ou outro tipo de conteúdo. Para criar, modificar ou excluir atribuições de função, use o portal da Web do SSRS. Após criar uma atribuição de função para um determinado usuário ou grupo, você pode modificá-la posteriormente selecionando uma função diferente. Para revogar permissões em um servidor de relatório, exclua uma atribuição de função desse servidor.  

Dependendo de seu objetivo, abordagens alternativas podem ser mais apropriadas. Os exemplos incluem a personalização ou a criação de uma nova definição de função ou a modificação da associação de uma conta de grupo no Active Directory.  

Por exemplo, suponha que você tenha um grupo de usuários que precisa gerenciar o conteúdo, mas não deve ter o conjunto completo de permissões associadas ao Gerenciador de Conteúdo. Você pode criar uma nova definição de função chamada Gerenciador de conteúdo do departamento. Ela pode incluir todas as tarefas no Gerenciador de conteúdo, exceto **Definir políticas de segurança para itens**.

Da mesma forma, se você for um administrador de sistema ou rede, provavelmente é mais fácil gerenciar as contas de grupo do Active Directory do que as atribuições de função no portal da Web. Você pode reduzir a sobrecarga de gerenciamento de atribuições de função criando uma atribuição de função única para uma conta de grupo. Em seguida, você pode modificar a associação de grupo quando os usuários não precisarem mais acessar os relatórios.
  
 Se você considerar a modificação ou a exclusão de uma atribuição de função como a melhor abordagem, verifique as atribuições de função de sistema e de item. Cada tipo de atribuição de função é configurado em páginas diferentes do portal da Web.
  
## <a name="to-modify-or-delete-a-system-role-assignment"></a>Para modificar ou excluir uma atribuição de função de sistema
  
1. Acesse [o portal da Web de um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/web-portal-ssrs-native-mode.md).

2. Selecione **Configurações de Site** > **Segurança**. Todas as atribuições de função do nível de sistema definidas atualmente para a implantação de servidor ou de expansão são listadas pelo nome de conta.

3. Localize a atribuição de função que deseja modificar ou excluir.

4. Para adicionar ou remover a função para um usuário ou grupo específico, selecione **Editar**.

5. Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e, em seguida, selecione **Excluir**.

### <a name="to-modify-or-delete-an-item-role-assignment"></a>Para modificar ou excluir uma atribuição de função de item

1. Acesse o portal da Web e localize o item para o qual você deseja editar ou excluir uma atribuição de função.

2. Focalize o item e selecione a seta do menu suspenso.

3. No menu suspenso, selecione **Segurança**.

4. Localize a atribuição de função que deseja modificar ou excluir.

5. Para adicionar ou remover a função para um usuário ou grupo específico, selecione **Editar**.

6. Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e, em seguida, selecione **Excluir**.

## <a name="see-also"></a>Confira também

[Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)  
[Atribuições de função](../../reporting-services/security/role-assignments.md)  
