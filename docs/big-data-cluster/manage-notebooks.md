---
title: Gerenciar um cluster de Big Data do SQL Server com os notebooks do Azure Data Studio
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Use um notebook do Azure Data Studio para gerenciar e solucionar problemas de um cluster de Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb2fcaf7431b5d79698af009b533ee49254777fe
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846653"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Gerenciar clusters de Big Data do SQL Server com os notebooks do Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornece uma extensão para o Azure Data Studio que inclui notebooks. Um notebook inclui documentação e código que você pode usar no Azure Data Studio para gerenciar clusters de Big Data para o SQL Server.

Originalmente implementados como um projeto de software livre, os [notebooks](notebooks-guidance.md) foram implementados no [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). Você pode usar markdown de texto nas células de texto e um dos kernels disponíveis para escrever código nas células de código.

Você pode usar notebooks para implantar clusters de Big Data para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Além dos notebooks, os usuários podem exibir uma coleção de blocos de anotações, que são chamados de livros de Jupyter. Um Jupyter Book fornece um sumário para navegar em uma coleção de notebooks. Dessa forma, um usuário encontra facilmente o notebook de que precisa, se deseja solucionar problemas no SQL Server ou exibir o status do cluster.

## <a name="prerequisites"></a>Pré-requisitos

Os pré-requisitos a seguir são necessários para poder iniciar o notebook:

* Versão mais recente do [build do Azure Data Studio Insiders](https://aka.ms/azuredatastudio-rc)
* Extensão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada no Azure Data Studio

Além disso, a implantação do cluster de Big Data do SQL Server 2019 também requer:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>Acesso aos notebooks de solução de problemas
Há três maneiras de acessar os notebooks de solução de problemas.

### <a name="command-palette"></a>Paleta de Comandos
1. Clique em **Exibir** e na **paleta de comandos**
2. Digite "Jupyter Books: Guia do SQL Server 2019 "
3. Isso abrirá os livros do Jupyter Viewlet com o livro Jupyter que contém os TSG relacionados a SQL Server clusters de Big Data.

### <a name="sql-master-dashboard"></a>Painel mestre do SQL
1. Depois de instalar o Azure Data Studio Insiders, conecte-se a uma instância de cluster de Big Data do SQL Server.
2. Depois de se conectar com êxito, clique com o botão direito do mouse no nome do servidor nas Conexões viewlet e clique em **Gerenciar**.
3. No painel, clique em **Cluster de Big Data do SQL Server**. Clique no **guia do SQL Server 2019** para abrir o Jupyter Book com os notebooks necessários.
    ![botão](media/manage-notebooks/jupyter-book-button.png)

1. Isso abrirá os livros do Jupyter Viewlet com o catálogo Jupyter do TSG já aberto.
4. Clique no notebook da tarefa que você precisa concluir.

### <a name="controller-dashboard"></a>Painel do controlador
1. No modo de exibição **conexões** , expanda **SQL Server clusters de Big Data.**
2. Adicionar detalhes do ponto de extremidade do controlador.
3. Após a conexão bem-sucedida com o controlador, clique com o botão direito do mouse no ponto de extremidade e clique em **gerenciar.**
4. Após o carregamento do painel, clique em solucionar problemas para iniciar o Jupyter do catálogo do TSG.

## <a name="how-to-use-troubleshooting-notebooks"></a>Como usar os notebooks de solução de problemas
1. Examine o Sumário do livro de Jupyter existente até encontrar o TSG que você precisa.
1. Todos os blocos de anotações são otimizados onde o usuário só precisa clicar em **células de execução.** Isso executará cada célula no bloco de anotações individualmente até que seja concluída.
1. Se você encontrar um erro, o livro Jupyter sugere um bloco de anotações que você pode executar para corrigir o erro. Siga as etapas e execute novamente o bloco de anotações.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre notebooks no Azure Data Studio, confira [Como usar notebooks na versão prévia do SQL Server 2019](notebooks-guidance.md).
