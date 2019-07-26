---
title: Criar um logon para SQLRUserGroup
description: Para conexões de loopback usando a autenticação implícita, crie um logon no SQL Server para SQLRUserGroup, para que uma conta de trabalho possa fazer logon no servidor, para conversão de identidade de volta para o usuário de chamada.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f86bedc3cfd92272b500d5d3edd701b6ca51d38b
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469984"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Criar um logon para SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Crie um [logon em SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando uma [conexão de retorno de loop](../../advanced-analytics/concepts/security.md#implied-authentication) em seu script especificar uma *conexão confiável*e a identidade usada para executar um objeto contiver seu código é uma conta de usuário do Windows.

As conexões confiáveis são aquelas `Trusted_Connection=True` que têm na cadeia de conexão. Quando SQL Server recebe uma solicitação especificando uma conexão confiável, ele verifica se a identidade do usuário atual do Windows tem um logon. Para processos externos executados como uma conta de trabalho (como MSSQLSERVER01 de **SQLRUserGroup**), a solicitação falha porque essas contas não têm um logon por padrão.

Você pode contornar o erro de conexão criando um logon para **SQLServerRUserGroup**. Para obter mais informações sobre identidades e processos externos, consulte [visão geral de segurança para a estrutura de extensibilidade](../concepts/security.md).

> [!Note]
> Verifique se **SQLRUserGroup** tem permissões de "permitir logon local". Por padrão, esse direito é fornecido a todos os novos usuários locais, mas algumas organizações de grupo mais rígidas podem desabilitar esse direito.

## <a name="create-a-login"></a>Criar um logon

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.

2. Na caixa de diálogo **logon – novo** , selecione **Pesquisar**. (Não digite nada na caixa ainda.)
    
     ![Clique em Pesquisar para adicionar um novo logon para o Machine Learning](media/implied-auth-login1.png "Clique em Pesquisar para adicionar um novo logon para o Machine Learning")

3. Na caixa **Selecionar usuário ou grupo** , clique no botão **tipos de objeto** .

     ![Pesquisar tipos de objeto para adicionar novo logon para aprendizado de máquina](media/implied-auth-login2.png "Pesquisar tipos de objeto para adicionar novo logon para aprendizado de máquina")

4. Na caixa de diálogo **tipos de objeto** , selecione **grupos**. Desmarque todas as outras caixas de seleção.

     ![Caixa de diálogo Selecionar grupos em tipos de objetos](media/implied-auth-login3.png "Caixa de diálogo Selecionar grupos em tipos de objetos")

4. Clique em **avançado**, verifique se o local para Pesquisar é o computador atual e clique em **localizar agora**.

     ![Clique em localizar agora para obter a lista de grupos](media/implied-auth-login4.png "Clique em localizar agora para obter a lista de grupos")

5. Percorra a lista de contas de grupo no servidor até encontrar uma começando com `SQLRUserGroup`.
    
    + O nome do grupo associado ao serviço Launchpad para a _instância padrão_ é sempre **SQLRUserGroup**, independentemente de você ter instalado o R ou Python ou ambos. Selecione esta conta somente para a instância padrão.
    + Se você estiver usando uma _instância nomeada_, o nome da instância será anexado ao nome do nome do grupo de trabalho padrão, `SQLRUserGroup`. Por exemplo, se sua instância for denominada "MLTEST", o nome do grupo de usuários padrão para essa instância será **SQLRUserGroupMLTest**.
 
    ![Exemplo de grupos no servidor](media/implied-auth-login5.png "Exemplo de grupos no servidor")
   
5. Clique em **OK** para fechar a caixa de diálogo pesquisa avançada.

    > [!IMPORTANT]
    > Verifique se você selecionou a conta correta para a instância. Cada instância pode usar apenas seu próprio serviço Launchpad e o grupo criado para esse serviço. As instâncias não podem compartilhar um serviço Launchpad ou contas de trabalho.

6. Clique em **OK** mais uma vez para fechar a caixa de diálogo **Selecionar usuário ou grupo** .

7. Na caixa de diálogo **logon – novo** , clique em **OK**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.

## <a name="next-steps"></a>Próximas etapas

+ [Visão geral de segurança](../concepts/security.md)
+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)
