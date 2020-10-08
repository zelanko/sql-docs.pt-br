---
title: 'Gerenciar: Notebooks do Azure Data Studio'
titleSuffix: SQL Server Big Data Clusters
description: Use um notebook no Azure Data Studio para gerenciar e solucionar problemas de Clusters de Big Data do SQL Server.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e54c9b01a58ba6eeeeda2fb74ca422d9d90ae45c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725770"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Gerenciar Clusters de Big Data do SQL Server com notebooks do Azure Data Studio

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornece uma extensão para o Azure Data Studio que inclui notebooks. Um notebook fornece a documentação e o código que você pode usar no Azure Data Studio para gerenciar Clusters de Big Data para o SQL Server 2019.

Originalmente implementados como um projeto de open-source, os [notebooks](../azure-data-studio/notebooks/notebooks-guidance.md) foram incorporados no [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md?view=sql-server-ver15). Você pode usar markdown de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar notebooks para implantar clusters de Big Data para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Além dos notebooks, você pode exibir uma coleção de notebooks, que são chamados de Jupyter Books. Um Jupyter Book fornece um sumário para ajudar você a navegar em uma coleção de notebooks. Dessa forma, você encontra facilmente o notebook de que precisa, seja para solucionar problemas no SQL Server ou para exibir o status do cluster.

## <a name="prerequisites"></a>Pré-requisitos

Você precisa desses pré-requisitos para abrir um notebook:

* A versão mais recente do [build do Azure Data Studio Insiders](./deploy-big-data-tools.md?viewFallbackFrom=sqlallproducts)
* A extensão [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], instalada no Azure Data Studio

Além desses pré-requisitos, para implantar Clusters de Big Data do SQL Server 2019, você também precisa de:

* [azdata](../azdata/install/deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>Acesso aos notebooks de solução de problemas

Há três maneiras de acessar os notebooks de solução de problemas.

### <a name="command-palette"></a>Paleta de Comandos

1. Selecione **Exibir** > **Paleta de Comandos**.

2. Insira **Jupyter Books: SQL Server 2019 Guide**.

Os manuais do viewlet do Jupyter Books com Jupyter Book que contém os notebooks de solução de problemas relacionados aos Clusters de Big Data do SQL Server serão abertos.

### <a name="sql-master-dashboard"></a>Painel Mestre do SQL

1. Depois de instalar o Azure Data Studio Insiders, conecte-se a uma instância dos Clusters de Big Data do SQL Server.

2. Após se conectar à instância, clique com o botão direito do mouse no nome do servidor em **CONEXÕES** e selecione **Gerenciar**.

3. No painel, selecione **Cluster de Big Data do SQL Server**. Selecione **guia do SQL Server 2019** para abrir o Jupyter Book que contém os notebooks necessários.
    ![Jupyter notebooks no painel](media/manage-notebooks/jupyter-book-button.png)

4. Selecione o notebook da tarefa que você precisa concluir.

### <a name="controller-dashboard"></a>Painel do controlador

1. Na exibição **Conexões**, expanda **Clusters de Big Data do SQL Server**.

2. Adicionar detalhes do ponto de extremidade do controlador.

3. Depois que estiver conectado ao controlador, clique com o botão direito do mouse no ponto de extremidade e selecione **Gerenciar**.

4. Depois que o painel for carregado, selecione **solucionar problemas** para abrir os guias de solução de problemas do Jupyter Book.

## <a name="use-troubleshooting-notebooks"></a>Usar notebooks de solução de problemas

1. Encontre o guia de solução de problemas de que você precisa no sumário do Jupyter Book.

2. Os notebooks são otimizados, portanto, você só precisa selecionar **Executar Células**. Esta ação executará cada célula no notebook individualmente até que ele seja concluído.

3. Se um erro for encontrado, o Jupyter Book sugerirá um notebook que você pode executar para corrigir o erro. Siga as etapas recomendadas e, em seguida, execute o notebook novamente.

## <a name="change-the-big-data-cluster"></a>Alterar um cluster de Big Data

Para alterar o cluster de Big Data do SQL Server para um notebook:

1. Clique no menu **Anexar a** da barra de ferramentas do notebook.

   ![Clique no menu Anexar a na barra de ferramentas do notebook](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Clique em um servidor no menu **Anexar a**.

   ![Selecione um servidor no menu Anexar a](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os notebooks no Azure Data Studio, confira [Como usar notebooks com o SQL Server](../azure-data-studio/notebooks/notebooks-guidance.md).