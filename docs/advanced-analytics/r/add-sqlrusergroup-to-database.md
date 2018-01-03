---
title: "Adicionar SQLRUserGroup como um usuário de banco de dados | Microsoft Docs"
ms.custom: 
ms.date: 12/21/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "autenticação implícita"
- SQLRUserGroup
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 7de60bccb72364e124656f03f043c03e812187db
ms.sourcegitcommit: ed9335fe62c0c8d94ee87006c6957925d09ee301
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>Adicionar SQLRUserGroup como um usuário de banco de dados

Este artigo explica como dar ao grupo de contas de trabalho usado por serviços de aprendizado de máquina no SQL Server as permissões necessárias para se conectar ao banco de dados e executar trabalhos de R ou Python em nome do usuário.

## <a name="what-is-sqlrusergroup"></a>O que é SQLRUserGroup?

Durante a instalação do [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] ou [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], novas contas de usuário do Windows são criadas para dar suporte à execução de R ou o token de segurança de tarefas de script de Python a [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço.

Você pode exibir essas contas no grupo de usuário do Windows **SQLRUserGroup**. Por padrão, 20 contas de trabalho são criadas, que geralmente é mais do que suficiente para executar o aprendizado de máquina de trabalhos.

Quando um usuário envia uma script de um cliente externo, de aprendizado de máquina [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ativa uma conta de trabalho disponível, ele é mapeado para a identidade do usuário da chamada e executa o script em nome do usuário. Esse novo serviço do mecanismo de banco de dados oferece suporte à execução segura de scripts externos, chamado *autenticação implícita*.

No entanto, se você precisa executar os scripts de R ou Python de um cliente de ciência de dados remotos, e você estiver usando autenticação do Windows, você deve atribuir essas contas de trabalho permissão para entrar para a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância em seu nome.

## <a name="add-sqlrusergroup-as-a-sql-server-login"></a>Adicionar SQLRUserGroup como um logon do SQL Server

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.

2. No **logon - novo** caixa de diálogo, selecione **pesquisa**. (Não digite nada na caixa ainda.)
    
     ![Clique em Pesquisar para adicionar um novo logon para o aprendizado de máquina](media/implied-auth-login1.png "clique em Pesquisar para adicionar um novo logon para o aprendizado de máquina")

3. No **Selecionar usuário ou grupo** , clique o **tipos de objeto** botão.

     ![Pesquisar tipos de objeto para adicionar um novo logon para o aprendizado de máquina](media/implied-auth-login2.png "pesquisar tipos de objeto para adicionar um novo logon para o aprendizado de máquina")

4. No **tipos de objeto** caixa de diálogo, selecione **grupos**. Desmarque todas as outras caixas de seleção.

     ![Selecione grupos na caixa de diálogo tipos de objeto](media/implied-auth-login3.png "selecionar grupos na caixa de diálogo tipos de objeto")

4. Clique em **avançado**, verifique se o local de pesquisa é o computador atual e clique **Localizar agora**.

     ![Clique em Localizar agora para obter uma lista de grupos de](media/implied-auth-login4.png "clique em Localizar agora para obter lista de grupos")

5. Percorra a lista de contas de grupo no servidor até encontrar um que começa com `SQLRUserGroup`.
    
    + O nome do grupo associada com o serviço barra inicial para o _instância padrão_ é sempre **SQLRUserGroup**, independentemente de se você instalou o R, Python ou ambos. Selecione esta conta somente a instância padrão.
    + Se você estiver usando um _instância nomeada_, o nome da instância é anexado ao nome do nome do grupo de trabalho padrão, `SQLRUserGroup`. Portanto, se a instância é chamada "MLTEST", o nome do grupo de usuário padrão para esta instância seria **SQLRUserGroupMLTest**.
 
     ![Exemplo de grupos no servidor](media/implied-auth-login5.png "exemplo de grupos no servidor")
   
5. Clique em **Okey** para fechar a caixa de diálogo de pesquisa avançada.

    > [!IMPORTANT]
    > Certifique-se de que você selecionou a conta correta para a instância. Cada instância pode usar seu próprio serviço de barra inicial e o grupo criado para esse serviço. Instâncias não podem compartilhar contas de serviço ou de trabalho de barra inicial.

6. Clique em **Okey** mais uma vez para fechar o **Selecionar usuário ou grupo** caixa de diálogo.

7. No **logon - novo** caixa de diálogo, clique em **Okey**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.

## <a name="change-the-number-of-worker-accounts-in-sqlrusergroup"></a>Alterar o número de contas de trabalho no SQLRUserGroup

Se você pretende fazer um uso intenso de aprendizado de máquina, você pode aumentar o número de contas usadas para executar scripts externos, como descrito neste artigo: 

+ [Modificar o pool de conta de usuário para o aprendizado de máquina](modify-the-user-account-pool-for-sql-server-r-services.md)

Por padrão, são criadas 20 contas, que oferece suporte a 20 sessões simultâneas. Tarefas em paralelo não consomem contas adicionais. Por exemplo, se um usuário executa uma tarefa de classificação que usa o processamento paralelo, a mesma conta de trabalho é reutilizada para todos os threads.
