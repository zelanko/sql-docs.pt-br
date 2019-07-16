---
title: Crie um logon para SQLRUserGroup - serviços do SQL Server Machine Learning
description: Para conexões de loopback usando autenticação implícita, crie um logon no SQL Server para SQLRUserGroup, para que uma conta de trabalho pode fazer logon no servidor, para conversão de identidade para o usuário que está chamando.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 7dafb4c9edfe830a354da61b72d330d800349781
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962353"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Criar um logon para SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Criar uma [logon no SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando uma [loop conexão back-](../../advanced-analytics/concepts/security.md#implied-authentication) em seu script especifica um *confiáveis conexão*, e a identidade usada para executar um objeto que contém o código é uma conta de usuário do Windows.

Confiáveis conexões são aqueles que `Trusted_Connection=True` na cadeia de conexão. Quando o SQL Server recebe uma solicitação especificar uma conexão confiável, ele verifica se a identidade do usuário atual do Windows tem um logon. Para execução como uma conta de trabalho de processos externos (como MSSQLSERVER01 partir **SQLRUserGroup**), a solicitação falha porque essas contas não têm um logon por padrão.

Você pode contornar o erro de conexão com a criação de um logon para **SQLServerRUserGroup**. Para obter mais informações sobre as identidades e processos externos, consulte [visão geral de segurança para a estrutura de extensibilidade](../concepts/security.md).

> [!Note]
> Certifique-se de que **SQLRUserGroup** tem permissões de "Permitir logon localmente". Por padrão, esse direito é fornecido para todos os novos usuários locais, mas algumas políticas de grupo mais rígidas que as organizações podem desabilitar esse direito.

## <a name="create-a-login"></a>Criar um logon

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.

2. No **logon - novo** caixa de diálogo, selecione **pesquisa**. (Não digite nada na caixa ainda.)
    
     ![Clique em Pesquisar para adicionar o novo logon para o machine learning](media/implied-auth-login1.png "clique em Pesquisar para adicionar o novo logon para o machine learning")

3. No **Selecionar usuário ou grupo** , clique o **tipos de objeto** botão.

     ![Pesquisar tipos de objeto para adicionar o novo logon para o machine learning](media/implied-auth-login2.png "pesquisar tipos de objeto para adicionar o novo logon para o machine learning")

4. No **tipos de objetos** caixa de diálogo, selecione **grupos**. Desmarque todas as outras caixas de seleção.

     ![Selecione grupos na caixa de diálogo tipos de objetos](media/implied-auth-login3.png "selecionar grupos na caixa de diálogo tipos de objeto")

4. Clique em **Advanced**, verifique se o local de pesquisa é o computador atual e clique **Localizar agora**.

     ![Clique em Localizar agora para obter uma lista dos grupos](media/implied-auth-login4.png "clique em Localizar agora para obter a lista de grupos")

5. Percorra a lista de contas de grupo no servidor até encontrar uma que começa com `SQLRUserGroup`.
    
    + O nome do grupo que está associada com o serviço Launchpad a _instância padrão_ é sempre **SQLRUserGroup**, independentemente de se você instalou o R ou Python ou ambos. Selecione essa conta somente a instância padrão.
    + Se você estiver usando um _instância nomeada_, o nome da instância é acrescentado ao nome do nome do grupo de trabalho padrão, `SQLRUserGroup`. Por exemplo, se a instância é denominada "MLTEST", o nome do grupo de usuário padrão para essa instância seria **SQLRUserGroupMLTest**.
 
    ![Exemplo de grupos no servidor](media/implied-auth-login5.png "exemplo de grupos no servidor")
   
5. Clique em **Okey** para fechar a caixa de diálogo de pesquisa avançada.

    > [!IMPORTANT]
    > Certifique-se de que você selecionou a conta correta para a instância. Cada instância pode usar apenas seu próprio serviço Launchpad e o grupo criado para o serviço. Instâncias não podem compartilhar contas de serviço ou de trabalho de barra inicial.

6. Clique em **Okey** mais uma vez para fechar o **Selecionar usuário ou grupo** caixa de diálogo.

7. No **logon - novo** caixa de diálogo, clique em **Okey**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.

## <a name="next-steps"></a>Próximas etapas

+ [Visão geral de segurança](../concepts/security.md)
+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)
