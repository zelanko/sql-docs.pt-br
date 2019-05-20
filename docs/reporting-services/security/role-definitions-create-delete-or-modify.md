---
title: Criar, excluir ou modificar uma função (Management Studio) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f079b7b16f485b92c60952d082281a1dba52d024
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570550"
---
# <a name="role-definitions---create-delete-or-modify"></a>Definições de função – Criar, excluir ou modificar

O Reporting Services fornece funções predefinidas que definem níveis de acesso ao servidor de relatório. Cada usuário ou grupo que requer acesso ao servidor de relatório é atribuído a uma função que define as tarefas permitidas. As funções são definidas para o servidor de relatório como um todo. Você deve ser consistente ao definir como uma função é usada por todas as áreas do servidor de relatório.

Para criar, modificar ou excluir funções, é possível usar o [!INCLUDE[SQL Server Management Studio](../../includes/ssmanstudiofull-md.md)]. Você só pode excluir funções que não estejam em uso.

 Para atribuir usuários e grupos às funções criadas, use o Portal da Web SSRS. Para obter mais informações, confira [Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md).

> [!NOTE]  
>Se o servidor de relatório estiver configurado para o modo integrado do SharePoint e você estiver conectado ao site do SharePoint no qual o servidor de relatório está integrado, poderá exibir e modificar os níveis de permissão que controlam o acesso ao conteúdo e às operações do servidor de relatório.

## <a name="to-create-a-role-definition"></a>Para criar uma definição de função

1. No Pesquisador de Objetos, expanda um nó do servidor de relatório.

2. Expanda a pasta Segurança.

3. Se você estiver criando uma definição de função no nível do item, clique com o botão direito do mouse em **Funções** > **Nova Função**.

    Ou, se você estiver criando uma definição de função no nível do sistema, clique com o botão direito do mouse em **Funções do Sistema** > **Nova Função do Sistema**.

4. Digite um nome exclusivo para a função. Um nome deve conter pelo menos um caractere. Também pode incluir espaços e alguns símbolos, mas não os seguintes caracteres `[; : \ / @ & = + , $ / * < > | "]`.

5. Como opção, digite uma descrição. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], essa descrição só é visível nesta página. Os usuários que exibem esse item por meio do portal da Web podem ver essa descrição nessa ferramenta.

6. Selecione as tarefas que os membros dessa função podem executar.

7. Selecione **OK**.

### <a name="to-delete-or-modify-a-role-definition"></a>Para excluir ou modificar uma definição de função  

1. No Pesquisador de Objetos, expanda um nó do servidor de relatório.

2. Expanda a pasta Segurança.

3. Para excluir ou modificar uma definição de função no nível do item, execute uma das ações a seguir:

    1. Para excluir uma definição de função, clique com o botão direito do mouse no item e clique em **Excluir**. A caixa de diálogo **Excluir Itens do Catálogo** é exibida. Selecione **OK** para excluir a função.
  
    2. Para modificar uma definição de função, clique com o botão direito do mouse no item e clique em **Propriedades**. A página Geral da caixa de diálogo **Propriedades de Função do Usuário** é exibida.

         Selecione as tarefas que os membros dessa função podem executar e selecione **OK**.
  
4. Para excluir ou modificar uma definição de função no nível do sistema, expanda a pasta **Funções do Sistema** . Execute uma dessas ações:

- Para excluir uma definição de função do sistema, clique com o botão direito do mouse no item e selecione **Excluir**. A caixa de diálogo **Excluir Itens do Catálogo** é exibida. Selecione **OK** para excluir a função.

- Para modificar uma definição de função do sistema, clique com o botão direito do mouse no item e selecione **Propriedades**. A página Geral da caixa de diálogo **Propriedades de Função do Sistema** é exibida. Selecione as tarefas que os membros desta função podem executar e clique em **OK** para aplicar as alterações.

## <a name="see-also"></a>Confira também

 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
 [Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)  
 [Reporting Services no SQL Server Management Studio &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
