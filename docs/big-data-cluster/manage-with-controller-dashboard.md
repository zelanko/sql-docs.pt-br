---
title: Gerenciar Cluster de Big Data do SQL Server com o painel do controlador
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: Use um notebook do Azure Data Studio para gerenciar e solucionar problemas de um cluster de Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a78074b7e32df18de1308d2354d98079d074f9bf
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531938"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>Gerenciar clusters de Big Data para o painel do controlador do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Além de **azdata** e do notebook de status do cluster, há outra maneira de exibir o status de um Cluster de Big Data do SQL Server. Agora você pode adicionar o controlador de cluster de Big Data do SQL Server por meio do viewlet de **Conexões**. Isso permite que você tenha um painel para exibir a integridade do cluster.

![painel](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>Prerequisites

Os pré-requisitos a seguir são necessários para iniciar o notebook:

* Versão mais recente do [build do Azure Data Studio Insiders](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)
* Extensão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada no Azure Data Studio

Além disso, o Cluster de Big Data do SQL Server 2019 também requer:

* **azdata**
    - [Windows Installer](deploy-install-azdata-installer.md)
    - [Gerenciador de pacotes do Linux](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)

## <a name="add-sql-server-big-data-cluster-controller"></a>Adicionar o controlador de Cluster de Big Data do SQL Server

1. Clique no modo de exibição Conexões no painel esquerdo.
2. Na parte inferior do modo de exibição Conexões, clique em **Clusters de Big Data do SQL Server** para expandi-lo.
3. Clique em **Adicionar controlador do cluster de Big Data do SQL Server**. Isso abrirá uma nova caixa de diálogo.

## <a name="add-new-controller"></a>Adicionar Novo Controlador

1. Adicione o nome do cluster.
2. Adicione a URL do Serviço de Gerenciamento de Cluster. Isso pode ser encontrado na tabela de pontos de extremidade de serviço no painel do BDC ou pergunte ao administrador do cluster.
3. Adicione seu nome de usuário e a senha.

## <a name="launch-controller-dashboard"></a>Iniciar painel do controlador

1. Quando você adicionar o controlador com êxito, poderá exibi-lo em Clusters de Big Data do SQL Server.
2. Para iniciar o painel, clique com o botão direito do mouse no controlador e clique em **Gerenciar**.

## <a name="controller-dashboard"></a>Painel do controlador

1. No painel do controlador, há três componentes principais:

    - **Barra de ferramentas** na parte superior que contém ações para o painel.
    - **O painel de navegação** à esquerda que muda para as diferentes exibições no painel.
    - **Exibição** abrangendo a maior parte da página.

2. Na página **Visão geral do cluster de Big Data**, você pode ver:

    - As **propriedades do cluster** para ver informações sobre o cluster.
    - **Visão Geral do Cluster** para conferir a visão geral de alto nível de todos os componentes do cluster e quais não estão íntegros
    - Os **Pontos de Extremidade de Serviço** para copiar ou acessar serviços diferentes em seu Cluster de Big Data do SQL Server.

3. No painel **NAV,** você pode ver a lista de serviços e clicar em um para exibir detalhes adicionais do cluster. Essas são as mesmas exibições de quando você clica em um serviço na visão geral do cluster **.**

4. Cada exibição em **Detalhes do Cluster** consiste nos mesmos componentes da interface do usuário:

    - **Detalhes do Status de Integridade** que compartilham o estado e o status de integridade do componente.
    - **Métricas e Logs** para exibir métricas e logs adicionais por meio de Grafana e Kibana.

1. Se você exibir um componente que não está íntegro, clique em **solucionar problemas** na barra de ferramentas para iniciar um Jupyter Book contendo um notebook para ajudar a diagnosticar o problema.

## <a name="next-steps"></a>Next Steps

Para obter mais informações sobre o controlador, confira a [documentação do controlador](concept-controller.md).