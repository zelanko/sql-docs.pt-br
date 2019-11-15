---
title: Criar um logon para SQLRUserGroup
description: Para conexões de loopback usando a autenticação implícita, crie um logon no SQL Server para SQLRUserGroup, para que uma conta de trabalho possa fazer logon no servidor, para conversão de identidade de volta para o usuário de chamada.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5194f251b7ea47e0d9485446b8957e96037ded0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714958"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Criar um logon para SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Crie um [logon no SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando uma [conexão de loopback](../../advanced-analytics/concepts/security.md#implied-authentication) em seu script especificar uma *conexão confiável* e a identidade usada para executar um objeto que contém seu código for uma conta de usuário do Windows.

As conexões confiáveis são aquelas que têm `Trusted_Connection=True` na cadeia de conexão. Quando o SQL Server recebe uma solicitação especificando uma conexão confiável, ele verifica se a identidade do usuário atual do Windows tem um logon. Para processos externos em execução como uma conta de trabalho (como MSSQLSERVER01 de **SQLRUserGroup**), a solicitação falha porque essas contas não têm um logon por padrão.

Você pode contornar o erro de conexão criando um logon para **SQLServerRUserGroup**. Para obter mais informações sobre identidades e processos externos, confira [Visão geral de segurança para a estrutura de extensibilidade](../concepts/security.md).

> [!Note]
> Certifique-se de que **SQLRUserGroup** tenha permissões de "Permitir logon local". Por padrão, esse direito é fornecido a todos os novos usuários locais, mas as políticas de grupo mais rígidas de algumas organizações podem desabilitar esse direito.

## <a name="create-a-login"></a>Criar um logon

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.

2. Na caixa de diálogo **Logon – Novo**, selecione **Pesquisar**. (Não digite nada na caixa ainda.)
    
     ![Clique em Pesquisar para adicionar um novo logon para aprendizado de máquina](media/implied-auth-login1.png "Click search to add new login for machine learning")

3. Na caixa **Selecionar usuário ou grupo**, clique no botão **Tipos de objeto**.

     ![Pesquisar tipos de objeto para adicionar novo logon para aprendizado de máquina](media/implied-auth-login2.png "Search object types to add new login for machine learning")

4. Na caixa de diálogo **Tipos de objeto**, selecione **Grupos**. Limpe todas as caixas de seleção.

     ![Selecione Grupos na caixa de diálogo Tipos de objetos](media/implied-auth-login3.png "Select Groups in Object Types dialog box")

4. Clique em **Avançado**, verifique se a localização a ser pesquisada é o computador atual e clique em **Localizar agora**.

     ![Clique em Localizar agora para obter a lista de grupos](media/implied-auth-login4.png "Click Find Now to get list of groups")

5. Percorra a lista de contas de grupo no servidor até encontrar uma começando com `SQLRUserGroup`.
    
    + O nome do grupo associado ao serviço Launchpad para a _instância padrão_ é sempre **SQLRUserGroup**, independentemente de você ter instalado R, Python ou ambos. Selecione esta conta somente para a instância padrão.
    + Se você estiver usando uma _instância nomeada_, o nome da instância será anexado ao nome do grupo de trabalho padrão, `SQLRUserGroup`. Por exemplo, se a instância for denominada "MLTEST", o nome do grupo de usuários padrão para essa instância será **SQLRUserGroupMLTest**.
 
    ![Exemplo de grupos no servidor](media/implied-auth-login5.png "Example of groups on server")
   
5. Clique em **OK** para fechar a caixa de diálogo de pesquisa avançada.

    > [!IMPORTANT]
    > Verifique se você selecionou a conta correta para a instância. Cada instância pode usar apenas seu próprio serviço Launchpad e o grupo criado para esse serviço. As instâncias não podem compartilhar um serviço Launchpad ou contas de trabalho.

6. Clique em **OK** mais uma vez para fechar a caixa de diálogo **Selecionar usuário ou grupo**.

7. Na caixa de diálogo **Logon – Novo**, clique em **OK**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.

## <a name="next-steps"></a>Próximas etapas

+ [Visão geral de segurança](../concepts/security.md)
+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)
