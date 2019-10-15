---
title: Gerenciar SQL Server clusters de Big data com blocos de anotações de Azure Data Studio
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: Use um notebook do Azure Data Studio para gerenciar e solucionar problemas de um cluster de Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e22b16cf8658e53e6bdc5db0fcd82692f3730fc7
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313683"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Gerenciar SQL Server clusters de Big data com blocos de anotações de Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornece uma extensão para o Azure Data Studio que inclui notebooks. Um notebook fornece documentação e código que você pode usar em Azure Data Studio para gerenciar clusters de Big data do 2019 SQL Server.

Originalmente implementado como um projeto de software livre, os [blocos de anotações](notebooks-guidance.md) foram incorporados em [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Você pode usar markdown de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar notebooks para implantar clusters de Big Data para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Além dos notebooks, você pode exibir uma coleção de blocos de anotações, que é chamada de livro de Jupyter. Um livro do Jupyter fornece um sumário para ajudá-lo a navegar em uma coleção de blocos de anotações para que você possa encontrar facilmente o bloco de anotações de que precisa, se deseja solucionar problemas SQL Server ou exibir o status do cluster.

## <a name="prerequisites"></a>Pré-requisitos

Você precisa desses pré-requisitos para abrir um bloco de anotações:

* A versão mais recente da [compilação do Azure Data Studio insiders](https://aka.ms/azuredatastudio-rc)
* A extensão [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], instalada em Azure Data Studio

Além desses pré-requisitos, para implantar SQL Server clusters de Big data 2019, você também precisa de:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>Acessar os notebooks de solução de problemas
Há três maneiras de acessar os notebooks de solução de problemas.

### <a name="command-palette"></a>Paleta de Comandos
1. Selecione **exibir** > **paleta de comandos**.
2. Insira os livros **Jupyter: Guia SQL Server 2019 @ no__t-0.

Os manuais do Jupyter Viewlet com o Jupyter Book que contém os notebooks de solução de problemas relacionados ao SQL Server clusters de Big data serão abertos.

### <a name="sql-master-dashboard"></a>Painel mestre do SQL
1. Depois de instalar o Azure Data Studios, conecte-se a uma instância SQL Server clusters de Big Data.
2. Depois que você estiver conectado à instância do, clique com o botão direito do mouse no nome do servidor em **conexões** e selecione **gerenciar**.
3. No painel, selecione **SQL Server Cluster de Big data**. Selecione o **guia SQL Server 2019** para abrir o livro Jupyter que contém os blocos de anotações necessários.
    blocos de anotações ![Jupyter no painel @ no__t-1

1. Selecione o bloco de anotações para a tarefa que você precisa concluir.

### <a name="controller-dashboard"></a>Painel do controlador
1. No modo de exibição **conexões** , expanda **SQL Server clusters de Big data**.
2. Adicionar detalhes do ponto de extremidade do controlador.
3. Depois que você estiver conectado ao controlador, clique com o botão direito do mouse no ponto de extremidade e selecione **gerenciar**.
4. Depois que o painel for carregado, selecione **solucionar problemas** para abrir os guias de solução de problemas do livro Jupyter.

## <a name="use-troubleshooting-notebooks"></a>Usar blocos de anotações de solução de problemas
1. Encontre o guia de solução de problemas de que você precisa no Sumário do livro de Jupyter.
1. Os blocos de anotações são otimizados, portanto, você só precisa selecionar **células de execução**. Esta ação executará cada célula no bloco de anotações individualmente até que o bloco de anotações seja concluído.
1. Se um erro for encontrado, o livro Jupyter irá sugerir um bloco de anotações que você pode executar para corrigir o erro. Siga as etapas recomendadas e, em seguida, execute o bloco de anotações novamente.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre notebooks no Azure Data Studio, confira [Como usar notebooks na versão prévia do SQL Server 2019](notebooks-guidance.md).
