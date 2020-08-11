---
title: Introdução
titleSuffix: SQL Server Big Data Clusters
description: Conheça as etapas e os recursos para implantar Clusters de Big Data do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4caaacd2d71d00d874a793129eef2f4144f03190
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784298"
---
# <a name="get-started-with-big-data-clusters-2019-deployment"></a>Introdução à implantação de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo apresenta uma visão geral de como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]. O artigo apresenta conceitos e fornece uma estrutura para entender os cenários de implantação. Suas etapas de implantação específicas variam de acordo com suas opções de plataforma para o cliente e o servidor. Para ver uma introdução do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)

Para ver outros cenários de implantação do SQL Server, confira:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Contêineres do Docker](../linux/sql-server-linux-configure-docker.md)

## <a name="quick-introduction"></a>Introdução rápida 

Assista a este vídeo de 9 minutos para obter uma visão geral de como implantar clusters de Big data:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Clusters-deployment-overview/player?WT.mc_id=dataexposed-c9-niner]


> [!TIP]
> Para obter rapidamente um ambiente com o Kubernetes e o cluster de Big Data implantados para ajudar você a se familiarizar com suas funcionalidades, use um dos scripts de exemplo indicados na [seção sobre scripts](#scripts). Após a implantação, para gerenciar o cluster, use as [ferramentas de cliente](#tools) na seção a seguir.


## <a name="client-tools"></a><a id="tools"></a> Ferramentas de cliente

Os clusters de Big Data exigem um conjunto específico de ferramentas de cliente. Antes de implantar um cluster de Big Data no Kubernetes, você deve instalar as ferramentas necessárias para a implantação. Ferramentas específicas são necessárias para cenários diferentes. Cada artigo deve explicar as ferramentas de pré-requisito para executar uma tarefa específica. Para obter uma lista completa de ferramentas e links de instalação, confira [Instalar ferramentas de Big Data do SQL Server 2019](deploy-big-data-tools.md).

## <a name="kubernetes"></a>Kubernetes

Os clusters de Big Data são implantados como uma série de contêineres inter-relacionados que são gerenciados no [Kubernetes](https://kubernetes.io/docs/home). Você pode hospedar o Kubernetes de várias maneiras. Mesmo que você já tenha um ambiente Kubernetes existente, examine os requisitos relacionados para clusters de Big Data.

- **AKS (Serviço de Kubernetes do Azure)** : O AKS permite que você implante um cluster do Kubernetes gerenciado no Azure. Você só gerencia e mantém os nós de agente. Com o AKS, você não precisa provisionar seu próprio hardware para o cluster. Também é fácil usar um [script Python](quickstart-big-data-cluster-deploy.md) ou um [notebook de implantação](notebooks-deploy.md) para criar o cluster do AKS e implantar o cluster de Big Data em uma única etapa. Para obter mais informações sobre como configurar o AKS para uma implantação de cluster de Big Data, confira [Configurar o Serviço de Kubernetes do Azure para implantações de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](deploy-on-aks.md).

- **ARO (Red Hat OpenShift no Azure)** : o ARO permite que você implante um cluster do Red Hat OpenShift gerenciado no Azure. Você só gerencia e mantém os nós de agente. Com o ARO, você não precisa provisionar um hardware próprio para o cluster. Também é fácil usar um [script Python](quickstart-big-data-cluster-deploy-aro.md) para criar o cluster do ARO e implantar o cluster de Big Data em uma só etapa. Esse modelo de implantação foi introduzido no SQL Server 2019 CU5. 

- **Vários computadores**: Você também pode implantar o Kubernetes em vários computadores Linux, que podem ser servidores físicos ou máquinas virtuais. A ferramenta [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) pode ser usada para criar o cluster do Kubernetes. Você pode usar um [script de Bash](deployment-script-single-node-kubeadm.md) para automatizar esse tipo de implantação. Esse método funcionará bem se você já tiver uma infraestrutura existente que deseja usar para o cluster de Big Data. Para obter mais informações sobre o uso de implantações **kubeadm** com clusters de Big Data, confira [Configurar o Kubernetes em vários computadores para implantações de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](deploy-with-kubeadm.md).

- **Red Hat OpenShift**: implante em seu cluster Red Hat OpenShift. Para obter mais informações, confira [Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no OpenShift local e no Red Hat OpenShift no Azure](deploy-openshift.md). Esse modelo de implantação foi introduzido no SQL Server 2019 CU5.

## <a name="deploy-a-big-data-cluster"></a>Implantar um cluster de Big Data

Depois de configurar o Kubernetes, você implanta um cluster de Big Data com o comando `azdata bdc create`. Ao implantar, você pode usar várias abordagens diferentes.

- Se você estiver implantando em um ambiente de desenvolvimento/teste, poderá optar por usar uma das [configurações padrão](deployment-guidance.md#deploy) fornecidas pelo **azdata**.

- Para personalizar sua implantação, você pode criar e usar seus próprios [arquivos de configuração de implantação](deployment-guidance.md#configfile).

- Para uma instalação completamente autônoma, você pode passar todas as outras configurações em variáveis de ambiente. Para obter mais informações, confira [implantações autônomas](deployment-guidance.md#unattended).


## <a name="deployment-scripts"></a><a id="scripts"></a> Scripts de implantação

Os scripts de implantação podem ajudar a implantar clusters do Kubernetes e de Big Data em uma única etapa. Geralmente, eles também fornecem valores padrão para configurações de cluster de Big Data. Você pode personalizar qualquer script de implantação criando sua própria versão que configura a implantação do cluster de Big Data de forma diferente.

Os seguintes scripts de implantação estão disponíveis no momento:

- [Script Python – Implantar um cluster de Big Data no AKS (Serviço de Kubernetes do Azure)](quickstart-big-data-cluster-deploy.md)
- [Script de Bash – Implantar um cluster de Big Data em um cluster kubeadm de nó único](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>Notebooks de implantação

Você também pode implantar um cluster de Big Data executando um notebook do Azure Data Studio. Para obter mais informações sobre como usar um notebook para implantar no AKS, confira o seguinte artigo:

- [Implantar um cluster de Big Data com os notebooks do Azure Data Studio](notebooks-deploy.md).

## <a name="next-steps"></a>Próximas etapas

Depois de implantar com êxito um cluster de Big Data, [conecte-se ao cluster](connect-to-big-data-cluster.md) e considere [carregar dados de exemplo](tutorial-load-sample-data.md) para uso com várias orientações.
