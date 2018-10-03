---
title: Explore os recursos do SQL do Azure com o Gerenciador de recursos do Azure | Microsoft Docs
description: Aprenda a explorar e gerenciar o servidor SQL do Azure, BD SQL do Azure e instância gerenciada do SQL por meio do Gerenciador de recursos do Azure.
author: yanancai
ms.author: yanacai
manager: craigg
ms.date: 09/24/2018
ms.topic: quickstart
ms.prod: sql
ms.openlocfilehash: 11f693329a92187c09cf3d8e8f1b74e287435594
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "48037593"
---
# <a name="explore-azure-sql-resources-with-azure-resource-explorer"></a>Explore os recursos do SQL do Azure com o Gerenciador de recursos do Azure

Neste documento, você aprenderá como você pode explorar e gerenciar o servidor SQL do Azure, banco de dados SQL do Azure e recursos de instância gerenciada do SQL por meio do Gerenciador de recursos do Azure no [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

>[!NOTE]
>O Gerenciador de recursos do Azure terão suporte na versão prévia do SQL Server 2019 em outubro. Depois disso, você pode instalar a extensão de visualização por meio [Gerenciador de extensões](extensions.md) ou por meio das **arquivo** > **instalar pacote do pacote VSIX**.


## <a name="connect-to-azure"></a>Conectar-se para o Azure

Depois de instalar o plug-in de visualização do SQL, um ícone do Azure aparece na barra de menus à esquerda. Clique no ícone para abrir o Gerenciador de recursos do Azure. Se você não vir o ícone do Azure, clique com botão direito na barra de menus à esquerda e selecione **Azure Resource Explorer**.

### <a name="add-an-azure-account"></a>Adicionar uma conta do Azure

Para exibir os recursos SQL associados com uma conta do Azure, você deve primeiro adicionar a conta para [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

1. Abra **contas vinculadas** caixa de diálogo por meio do ícone de gerenciamento da conta no canto inferior esquerdo ou por meio de **entrar no Azure...**  link no Gerenciador de recursos do Azure.

    ![Entrar no Azure](media/azure-resource-explorer/sign-in-to-azure.png)

2. No **contas vinculadas** caixa de diálogo, clique em **adicionar uma conta**.

    ![Adicionar uma conta do Azure](media/azure-resource-explorer/add-an-azure-account.png)

3. Clique em **copiar e abrir** para abrir o navegador para autenticação.

    ![Página de autenticação aberta no navegador](media/azure-resource-explorer/open-authentication-in-browser.png)

4. Cole a **código do usuário** na página da web e clique **continuar** para autenticar.

    ![Autenticar no navegador](media/azure-resource-explorer/authenticate-in-browser.png)

5. Na [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] agora você deve encontrar o fez logon na conta do Azure no **contas vinculadas** caixa de diálogo.

    ![Conectado na conta do Azure](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>Adicione as contas do Azure mais

Várias contas do Azure têm suporte no [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]. Para adicionar as contas do Azure mais, clique no botão no canto superior direito da **contas vinculadas** caixa de diálogo e siga as mesmas etapas com adicionam uma seção de conta do Azure para adicionar as contas do Azure mais.

![Adicionar conta do Azure mais](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>Remover uma conta do Azure

Para remover uma conta do Azure conectada existente:

1. Abra **contas vinculadas** diálogo por meio do ícone de gerenciamento de conta no canto inferior esquerdo.
2. Clique o **X** botão à direita da conta do Azure para removê-lo.

    ![Remover conta do Azure](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>Filtro de assinatura

Após fazer logon uma conta do Azure, todas as assinaturas associados com essa exibição da conta do Azure no Gerenciador de recursos do Azure. Você pode filtrar as assinaturas para cada conta do Azure.

1. Clique o **selecionar assinatura** botão à direita da conta do Azure.

   ![Filtro de assinatura](media/azure-resource-explorer/filter-subscription.png)

2. Marque as caixas de seleção para as assinaturas de conta que você deseja procurar e, em seguida, clique em **Okey**.

   ![Selecionar assinatura](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>Explore os recursos do SQL do Azure

Para navegar de um recurso do SQL do Azure no Gerenciador de recursos do Azure, expanda as contas do Azure e o tipo de grupo de recursos.

O Gerenciador de recursos do Azure dá suporte ao Azure SQL Server, o banco de dados SQL e a instância gerenciada do SQL no momento.

## <a name="connect-to-azure-sql-resources"></a>Conectar-se aos recursos do SQL do Azure

O Gerenciador de recursos do Azure fornecem acesso rápido que ajuda você a se conectar a servidores SQL e bancos de dados para consulta e gerenciamento. 

1. Explore o recurso SQL que você gostaria de conectar-se com o modo de exibição de árvore.
2. Clique com botão direito do recurso e selecione **Connect**, você também pode encontrar o botão Conectar na parte direita do recurso.

   ![Conectar-se ao recurso de SQL do Azure](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. Em aberto **Conexão** caixa de diálogo, insira sua senha e clique em **Connect**.

   ![Caixa de diálogo de conexão SQL](media/azure-resource-explorer/sql-connection-dialog.png)
4. O **servidores** janela abre automaticamente com o novo SQL server/banco de dados conectado após a conexão bem-sucedida.

## <a name="next-steps"></a>Próximas etapas

- [Use [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] para se conectar e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Use [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] para se conectar e consultar dados no Azure SQL Data Warehouse](quickstart-sql-dw.md)