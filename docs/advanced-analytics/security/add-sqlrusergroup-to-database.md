---
title: Adicionar SQLRUserGroup como um usuário de banco de dados (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Para conexões de loopback usando autenticação implícita, adicione SQLRUserGroup como um usuário de banco de dados para que uma conta de trabalho pode fazer logon no servidor, para conversão de identidade para o usuário que está chamando.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4685288eb383c486556efba1eb4861ca9d708c0f
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419081"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>Adicionar SQLRUserGroup como um usuário de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Crie um logon de banco de dados para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando um [loop conexão back-](../../advanced-analytics/concepts/security.md#implied-authentication) em seu script especifica um *confiáveis conexão*e a identidade usada para executar um objeto contém o código é uma conta de usuário do Windows.

Confiáveis conexões são aqueles que `Trusted_Connection=True` na cadeia de conexão. Quando o SQL Server recebe uma solicitação especificar uma conexão confiável, ele verifica se a identidade do usuário atual do Windows tem um logon. Para execução como uma conta de trabalho de processos externos (como MSSQLSERVER01 partir **SQLRUserGroup**), a solicitação falha porque essas contas não têm um logon por padrão.

Você pode contornar o erro de conexão, fornecendo **SQLServerRUserGroup** um logon do SQL Server. Para obter mais informações sobre as identidades e processos externos, consulte [visão geral de segurança para a estrutura de extensibilidade](../concepts/security.md).

> [!Note]
>  Certifique-se de que **SQLRUserGroup** tem permissões de "Permitir logon localmente". Por padrão, esse direito é fornecido para todos os novos usuários locais, mas em algumas organizações, políticas de grupo mais rígidas podem desabilitar esse direito.

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