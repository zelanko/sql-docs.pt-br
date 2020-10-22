---
title: Criar um logon para SQLRUserGroup
description: Crie um logon no SQL Server para SQLRUserGroup, usando a autenticação implícita para fazer logon no servidor para conversão da identidade de volta para o usuário autor da chamada.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/25/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcdb8353abe029291352f031d5261849514ef8fd
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92195750"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Criar um logon para SQLRUserGroup
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Crie um [logon no SQL Server](../../relational-databases/security/authentication-access/create-a-login.md) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando uma [conexão de loopback](../../machine-learning/concepts/security.md#implied-authentication) em seu script especificar uma *conexão confiável* e a identidade usada para executar um objeto que contém seu código for uma conta de usuário do Windows.

As conexões confiáveis são aquelas que têm `Trusted_Connection=True` na cadeia de conexão. Quando o SQL Server recebe uma solicitação especificando uma conexão confiável, ele verifica se a identidade do usuário atual do Windows tem um logon. Para processos externos em execução como uma conta de trabalho (como MSSQLSERVER01 de **SQLRUserGroup**), a solicitação falha porque essas contas não têm um logon por padrão.

Você pode contornar o erro de conexão criando um logon para **SQLServerRUserGroup**. Para obter mais informações sobre identidades e processos externos, confira [Visão geral de segurança para a estrutura de extensibilidade](../concepts/security.md).

> [!Note]
> Certifique-se de que **SQLRUserGroup** tenha permissões de "Permitir logon local". Por padrão, esse direito é fornecido a todos os novos usuários locais, mas as políticas de grupo mais rígidas de algumas organizações podem desabilitar esse direito.

## <a name="create-a-login"></a>Criar um logon

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.

2. Na caixa de diálogo **Logon – Novo**, selecione **Pesquisar**. (Não digite nada na caixa ainda.)
    
     ![Clicar em Pesquisar para adicionar um novo logon para machine learning](media/implied-auth-login1.png "Clicar em Pesquisar para adicionar um novo logon para machine learning")

3. Na caixa **Selecionar usuário ou grupo**, clique no botão **Tipos de objeto**.

     ![Pesquisar tipos de objeto para adicionar um novo logon para machine learning](media/implied-auth-login2.png "Pesquisar tipos de objeto para adicionar um novo logon para machine learning")

4. Na caixa de diálogo **Tipos de objeto**, selecione **Grupos**. Limpe todas as caixas de seleção.

     ![Caixa de diálogo Selecionar grupos nos tipos de objetos](media/implied-auth-login3.png "Caixa de diálogo Selecionar grupos nos tipos de objetos")

4. Clique em **Avançado**, verifique se a localização a ser pesquisada é o computador atual e clique em **Localizar agora**.

     ![Clicar em Localizar agora para obter uma lista de grupos](media/implied-auth-login4.png "Clicar em Localizar agora para obter uma lista de grupos")

5. Percorra a lista de contas de grupo no servidor até encontrar uma começando com `SQLRUserGroup`.
    
    + O nome do grupo associado ao serviço Launchpad para a _instância padrão_ é sempre **SQLRUserGroup**, independentemente de você ter instalado R, Python ou ambos. Selecione esta conta somente para a instância padrão.
    + Se você estiver usando uma _instância nomeada_, o nome da instância será anexado ao nome do grupo de trabalho padrão, `SQLRUserGroup`. Por exemplo, se a instância for denominada "MLTEST", o nome do grupo de usuários padrão para essa instância será **SQLRUserGroupMLTest**.
 
    ![Exemplo de grupos no servidor](media/implied-auth-login5.png "Exemplo de grupos no servidor")
   
5. Clique em **OK** para fechar a caixa de diálogo de pesquisa avançada.

    > [!IMPORTANT]
    > Verifique se você selecionou a conta correta para a instância. Cada instância pode usar apenas seu próprio serviço Launchpad e o grupo criado para esse serviço. As instâncias não podem compartilhar um serviço Launchpad ou contas de trabalho.

6. Clique em **OK** mais uma vez para fechar a caixa de diálogo **Selecionar usuário ou grupo**.

7. Na caixa de diálogo **Logon – Novo**, clique em **OK**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.

## <a name="next-steps"></a>Próximas etapas

+ [Visão geral de segurança](../concepts/security.md)
+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)