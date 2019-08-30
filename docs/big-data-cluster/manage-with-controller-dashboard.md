---
title: Gerenciar SQL Server Cluster de Big Data com o painel do controlador
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: Use um notebook do Azure Data Studio para gerenciar e solucionar problemas de um cluster de Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 08/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5fadb9b069e6f70cb780e6dc69295f63330a683a
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160725"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>Gerenciar clusters de Big Data para o painel do controlador SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Além do **azdata** e do bloco de anotações de status do cluster, há outra maneira de exibir o status de um cluster SQL Server Big Data. Agora você pode adicionar o controlador de cluster SQL Server Big data por meio das **conexões** Viewlet. Isso permite que você tenha um painel para exibir a integridade do cluster.

![painel](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são necessários para iniciar o notebook:

* Versão mais recente do [build do Azure Data Studio Insiders](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)
* Extensão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] instalada no Azure Data Studio

Além de acima, SQL Server Cluster de Big data 2019 também requer:

* **azdata**
    - [Gerenciador de pacotes do Linux](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [CLI do Azure](/cli/azure/install-azure-cli)


## <a name="add-sql-server-big-data-cluster-controller"></a>Adicionar SQL Server Big Data controlador de cluster

1. Clique no modo de exibição conexões no painel esquerdo.
2. Na parte inferior do modo de exibição conexões, clique em **SQL Server clusters de Big data** para expandi-lo.
3. Clique em **adicionar SQL Server Big data controlador de cluster**, isso abrirá uma nova caixa de diálogo.

## <a name="add-new-controller"></a>Adicionar novo controlador

1. Adicione o nome do cluster.
2. Adicione a URL do serviço de gerenciamento de cluster. Isso pode ser encontrado na tabela de pontos de extremidade de serviço no painel do BDC ou pergunte ao administrador do cluster.
3. Adicione seu nome de usuário e senha.

## <a name="launch-controller-dashboard"></a>Iniciar painel do controlador

1. Quando você adicionar o controlador com êxito, poderá exibi-lo em clusters de Big data SQL Server.
2. Para iniciar o painel, clique com o botão direito do mouse no controlador e clique em **gerenciar**.

## <a name="controller-dashboard"></a>Painel do controlador

1. No painel do controlador, há três componentes principais:

    - **Barra de ferramentas** na parte superior que contém ações para o painel.
    - **Painel de navegação** à esquerda que muda para as diferentes exibições no painel.
    - **Exibição** que abrange a maioria da página.

2. Na página **visão geral do cluster de Big data** , você pode ver:

    - **Propriedades do cluster** para ver informações sobre o cluster.
    - **Visão geral do cluster** para ver a visão geral de alto nível de todos os componentes do cluster e quais deles não estão íntegros
    - **Pontos de extremidade de serviço** para copiar ou acessar serviços diferentes em seu SQL Server Cluster de Big Data.

3. No **painel de navegação,** você pode ver a lista de serviços e clicar em um para exibir detalhes adicionais do cluster. Essas são as mesmas exibições quando você clica em um serviço na **visão geral do cluster.**

4. Cada exibição em **detalhes do cluster** consiste nos mesmos componentes da interface do usuário:

    - **Detalhes do status de integridade** que compartilham o estado e o status de integridade do componente.
    - **Métricas e logs** para exibir métricas e logs adicionais por meio de Grafana e Kibana.

1. Se você exibir um componente que não está íntegro, clique em **solucionar problemas** na barra de ferramentas para iniciar um livro Jupyter contendo um bloco de anotações para ajudar a diagnosticar o problema.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o controlador, consulte a [documentação do controlador](concept-controller.md).