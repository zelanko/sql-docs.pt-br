---
title: Gerenciar um cluster de Big Data do SQL Server com os notebooks do Azure Data Studio
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use um notebook do Azure Data Studio para gerenciar e solucionar problemas de um cluster de Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d9c8edd91ced01135d740fecdf6cf837df9cac6b
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470726"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Gerenciar clusters de Big Data do SQL Server com os notebooks do Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornece uma extensão para o Azure Data Studio que inclui notebooks. Um notebook inclui documentação e código que você pode usar no Azure Data Studio para gerenciar clusters de Big Data para o SQL Server.

Originalmente implementados como um projeto de software livre, os [notebooks](notebooks-guidance.md) foram implementados no [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). Você pode usar markdown de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar notebooks para implantar clusters de Big Data para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Além dos notebooks, os usuários podem exibir uma coleção de notebooks, que são chamados de Jupyter Books. Um Jupyter Book fornece um sumário para navegar em uma coleção de notebooks. Dessa forma, um usuário encontra facilmente o notebook de que precisa, se deseja solucionar problemas no SQL Server ou exibir o status do cluster.

## <a name="prerequisites"></a>Prerequisites

Os pré-requisitos a seguir são necessários para poder iniciar o notebook:

* Versão mais recente do [build do Azure Data Studio Insiders](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)
* Extensão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada no Azure Data Studio

Além disso, a implantação do cluster de Big Data do SQL Server 2019 também requer:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>Acesso aos notebooks de solução de problemas

1. Depois de instalar o Azure Data Studio Insiders, conecte-se a uma instância de cluster de Big Data do SQL Server.
2. Depois de se conectar com êxito, clique com o botão direito do mouse no nome do servidor nas Conexões viewlet e clique em **Gerenciar**.
3. No painel, clique em **Cluster de Big Data do SQL Server**. Clique no **guia do SQL Server 2019** para abrir o Jupyter Book com os notebooks necessários.
    ![botão](media/manage-notebooks/jupyter-book-button.png)

1. Na janela do seletor de pasta, escolha uma localização para salvar seu Jupyter Book.
2. Clique em **Recarregar** para recarregar o Azure Data Studio e ver seu Jupyter Book. Clique em **Abrir nova instância** para abrir uma nova instância do Azure Data Studio com o Jupyter Book.
3. No modo de exibição do Explorer, você deve ver uma seção chamada **Livros**. Se não estiver expandida, clique nela para exibir os notebooks.
4. Clique no notebook da tarefa que você precisa concluir.

## <a name="next-steps"></a>Next Steps
Para obter mais informações sobre notebooks no Azure Data Studio, confira [Como usar notebooks na versão prévia do SQL Server 2019](notebooks-guidance.md).