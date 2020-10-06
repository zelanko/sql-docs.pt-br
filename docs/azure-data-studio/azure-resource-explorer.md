---
title: Explorar os recursos do SQL do Azure com o Azure Resource Explorer
description: Saiba como explorar e gerenciar o SQL Server do Azure, o Banco de Dados SQL do Azure e a Instância Gerenciada do SQL do Azure por meio do Azure Resource Explorer.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yanancai
ms.author: yanacai
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 972e715de4ec8504c488ce70c47fecc3f04b3fca
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725227"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>Explorar e gerenciar recursos do SQL do Azure com o Azure Resource Explorer

Neste documento, você aprenderá a explorar e gerenciar os recursos do SQL Server do Azure, do Banco de Dados SQL do Azure e da Instância Gerenciada do SQL do Azure por meio do Azure Resource Explorer no [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

>[!NOTE]
>O Azure Resource Explorer tem suporte no SQL Server 2019. Depois disso, você poderá instalar a extensão por meio do [gerenciador de extensões](./extensions/add-extensions.md) ou de **Arquivo** > **Instalar Pacote do Pacote do VSIX**.

## <a name="connect-to-azure"></a>Conectar-se ao Azure

Após a instalação do plug-in do SQL, um ícone do Azure será exibido na barra de menus à esquerda. Clique no ícone para abrir o Azure Resource Explorer. Se o ícone do Azure não for exibido, clique com o botão direito do mouse na barra de menus à esquerda e selecione **Azure Resource Explorer**.

### <a name="add-an-azure-account"></a>Adicionar uma conta do Azure

Para exibir os recursos do SQL associados a uma conta do Azure, você deverá primeiro adicionar a conta ao [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

1. Abra a caixa de diálogo **Contas Vinculadas** por meio do ícone de gerenciamento de contas na parte inferior esquerda ou por meio do link **Entrar no Azure...** no Azure Resource Explorer.

    ![Entrar no Azure](media/azure-resource-explorer/sign-in-to-azure.png)

2. Na caixa de diálogo **Contas Vinculadas**, clique em **Adicionar uma conta**.

    ![Adicionar uma conta do Azure](media/azure-resource-explorer/add-an-azure-account.png)

3. Clique em **Copiar e Abrir** para abrir o navegador para autenticação.

    ![Abrir a página de autenticação no navegador](media/azure-resource-explorer/open-authentication-in-browser.png)

4. Cole o **Código do usuário** na página da Web e clique em **Continuar** para se autenticar.

    ![Autenticar-se no navegador](media/azure-resource-explorer/authenticate-in-browser.png)

5. No [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)], agora você deverá encontrar a conta conectada do Azure na caixa de diálogo **Contas Vinculadas**.

    ![Conta conectada do Azure](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>Adicionar mais contas do Azure

Há suporte para várias contas do Azure no [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]. Para adicionar mais contas do Azure, clique no botão na parte superior direita da caixa de diálogo **Contas Vinculadas** e siga as mesmas etapas com a seção Adicionar uma conta do Azure para adicionar mais contas do Azure.

![Adicionar mais contas do Azure](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>Remover uma conta do Azure

Para remover uma conta conectada do Azure existente:

1. Abra a caixa de diálogo **Contas Vinculadas** por meio do ícone gerenciamento de contas na parte inferior esquerda.
2. Clique no botão **X** à direita da conta do Azure para removê-la.

    ![Remover uma conta do Azure](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>Filtrar uma assinatura

Depois que você estiver conectado a uma conta do Azure, todas as assinaturas associadas a essa conta do Azure serão exibidas no Azure Resource Explorer. Você poderá filtrar assinaturas para cada conta do Azure.

1. Clique no botão **Selecionar Assinatura** à direita da conta do Azure.

   ![Filtrar uma assinatura](media/azure-resource-explorer/filter-subscription.png)

2. Marque as caixas de seleção das assinaturas de conta que deseja procurar e, em seguida, clique em **OK**.

   ![Selecionar uma assinatura](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>Explorar os recursos do SQL do Azure

Para navegar por um recurso do SQL do Azure no Azure Resource Explorer, expanda o grupo de tipos de recursos e contas do Azure.

Atualmente, o Azure Resource Explorer dá suporte ao SQL Server do Azure, ao Banco de Dados SQL do Azure e à Instância Gerenciada do SQL do Azure.

## <a name="connect-to-azure-sql-resources"></a>Conectar-se aos recursos do SQL do Azure

O Azure Resource Explorer fornece acesso rápido que ajuda você a se conectar a SQL Servers e bancos de dados para consulta e gerenciamento.

1. Explore o recurso do SQL com o qual deseja se conectar no modo de exibição de árvore.
2. Clique com o botão direito do mouse no recurso e selecione **Conectar**. Encontre também o botão Conectar à direita do recurso.

   ![Conectar-se ao recurso do SQL do Azure](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. Na caixa de diálogo **Conexão** aberta, insira sua senha e clique em **Conectar**.

   ![Caixa de diálogo de conexão do SQL](media/azure-resource-explorer/sql-connection-dialog.png)
4. A janela **Servidores** é aberta automaticamente com o novo SQL Server/banco de dados conectado depois que a conexão é estabelecida com êxito.

## <a name="next-steps"></a>Próximas etapas

- [Use [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] para conectar-se ao Banco de Dados SQL do Azure e consultá-lo](quickstart-sql-database.md)
- [Use [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] para conectar-se ao SQL Data Warehouse do Azure e consultá-lo](quickstart-sql-dw.md)