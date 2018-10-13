---
title: Adicionar SQLRUserGroup como um usuário de banco de dados (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Como adicionar SQLRUserGroup como um usuário de banco de dados para serviços do SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fc5294453def64d13cc43a74a8a5fb299c3e23e3
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100317"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>Adicionar SQLRUserGroup como um usuário de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Crie um logon de banco de dados para o [SQLRUserGroup](../concepts/security.md#sqlrusergroup) para permitir conexões confiáveis provenientes de scripts R e Python quando o destino é dados ou operações na instância do SQL Server. 

Para scripts que contêm cadeias de caracteres de conexão com logons do SQL Server ou um nome de usuário totalmente especificado e uma senha, não é necessário criar um logon.

## <a name="when-a-login-is-required"></a>Quando um logon é necessário

Se o script de R ou Python inclui uma cadeia de caracteres de conexão especificando uma conexão confiável (por exemplo, "Trusted_Connection = True"), configuração adicional é necessária para a apresentação correta da identidade do usuário para o SQL Server. Para processos externos em execução em um **SQLRUserGroup** conta de trabalho, como MSSQLSERVER01, o usuário confiável é apresentada como a identidade do trabalho. Como essa identidade não tem nenhum direito de logon para o SQL Server, o que é confiável conexões falhará a menos que você adicione **SQLRUserGroup** como um usuário de banco de dados. Para obter mais informações, consulte [ *autenticação implícita*](../../advanced-analytics/concepts/security.md#implied-authentication).

Lembre-se de que o Launchpad mantém um mapeamento do usuário original que invocado o script e a conta de trabalho que executa o processo. Depois que a conexão confiável for bem-sucedida para a conta de trabalho, a identidade do usuário da chamada original assume e é usada para recuperar os dados. Você não precisa conceder permissões db_datareader **SQLRUserGroup**.

> [!Note]
>  Certifique-se de que **SQLRUserGroup** tem permissões de "Permitir logon localmente". Por padrão, esse direito é fornecido para todos os novos usuários locais, mas em algumas organizações políticas mais rígidas do grupo podem ser impostas.

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
    + Se você estiver usando um _instância nomeada_, o nome da instância é acrescentado ao nome do nome do grupo de trabalho padrão, `SQLRUserGroup`. Portanto, se a instância é denominada "MLTEST", o nome do grupo de usuário padrão para essa instância seria **SQLRUserGroupMLTest**.
 
     ![Exemplo de grupos no servidor](media/implied-auth-login5.png "exemplo de grupos no servidor")
   
5. Clique em **Okey** para fechar a caixa de diálogo de pesquisa avançada.

    > [!IMPORTANT]
    > Certifique-se de que você selecionou a conta correta para a instância. Cada instância pode usar apenas seu próprio serviço Launchpad e o grupo criado para o serviço. Instâncias não podem compartilhar contas de serviço ou de trabalho de barra inicial.

6. Clique em **Okey** mais uma vez para fechar o **Selecionar usuário ou grupo** caixa de diálogo.

7. No **logon - novo** caixa de diálogo, clique em **Okey**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.