---
title: Configurar o Serviço de Kubernetes do Azure
titleSuffix: SQL Server Big Data Clusters
description: Saiba como configurar o AKS (Serviço de Kubernetes do Azure) para implantações de cluster de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 27e2596894e6d36742472ad1d3ae192fc37787e6
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489666"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>Configurar o Serviço de Kubernetes do Azure para implantações de cluster de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como configurar o AKS (Serviço de Kubernetes do Azure) para implantações [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

O AKS simplifica a criação, a configuração e o gerenciamento de um cluster de máquinas virtuais que são pré-configuradas com um cluster do Kubernetes para executar aplicativos em contêineres. Isso permite que você use suas habilidades existentes ou tire proveito de um corpo grande e crescente de experiência da comunidade, para implantar e gerenciar aplicativos baseados em contêiner no Microsoft Azure.

Este artigo descreve as etapas para implantar o Kubernetes no AKS usando a CLI do Azure. Caso não tenha uma assinatura do Azure, crie uma conta gratuita antes de começar.

> [!TIP]
> Você também pode criar o script da implantação do AKS e de um cluster de Big Data em uma única etapa. Para obter mais informações, confira como fazer isso em um [script Python](quickstart-big-data-cluster-deploy.md) ou em um [notebook](notebooks-deploy.md) do Azure Data Studio.

## <a name="prerequisites"></a>Pré-requisitos

- [Implantar as ferramentas de Big Data do SQL Server 2019](deploy-big-data-tools.md):
   - **Kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
   - **CLI do Azure**

- Versão mínima de 1.13 para o servidor do Kubernetes. No AKS, você precisa usar o parâmetro `--kubernetes-version` para especificar uma versão diferente do padrão.

- Para garantir uma implantação bem-sucedida e uma experiência ideal ao validar cenários básicos no AKS, você pode usar um único nó ou um cluster do AKS de vários nós, com estes recursos disponíveis:
   - 8 vCPUs em todos os nós
   - 64 GB de memória por VM
   - 24 ou mais discos anexados em todos os nós

   > [!TIP]
   > A infraestrutura do Azure oferece várias opções de tamanho para VMs. Confira [aqui](/azure/virtual-machines/windows/sizes) para seleções na região que você planeja implantar.

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados. As etapas a seguir entram no Azure e criam um grupo de recursos para o cluster do AKS.

1. No prompt de comando, execute o seguinte comando e siga os prompts para fazer logon em sua assinatura do Azure:

    ```azurecli
    az login
    ```

1. Se você tiver várias assinaturas, poderá exibir todas as suas assinaturas executando o seguinte comando:

   ```azurecli
   az account list
   ```

1. Se você quiser alterar para uma assinatura diferente, poderá executar este comando:

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. Identifique a região do Azure em que deseja implantar o cluster e os recursos usando este comando:

   ```azurecli
   az account list-locations -o table
   ```

1. Crie um grupo de recursos com o comando **az group create**. O exemplo a seguir cria um grupo de recursos chamado `sqlbdcgroup` na localização `westus2`.

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>Verificar as versões disponíveis do Kubernetes

Use a versão mais recente disponível do Kubernetes. A versão mais recente disponível depende da localização em que você está implantando o cluster. O comando a seguir retorna as versões do Kubernetes disponíveis em uma localização específica.

Antes de executar o comando, atualize o script. Substitua `<Azure data center>` pela localização do cluster.

   **Bash**

   ```bash
   az aks get-versions \
   --location <Azure data center> \
   --query orchestrators \
   --o table
   ```

   **PowerShell**

   ```powershell
   az aks get-versions `
   --location <Azure data center> `
   --query orchestrators `
   --o table
   ```

Escolha a versão mais recente disponível para o cluster. Registre o número de versão. Você o usará na próxima etapa.

## <a name="create-a-kubernetes-cluster"></a>Criar um cluster do Kubernetes

1. Crie um cluster do Kubernetes no AKS com o comando [az aks create](/cli/azure/aks). O exemplo a seguir cria um cluster do Kubernetes chamado *kubcluster* com um nó de agente do Linux de tamanho **Standard_L8s**.

   Antes de executar o script, substitua `<version number>` pelo número de versão identificado na etapa anterior.

   Crie o cluster do AKS no mesmo grupo de recursos que você usou nas seções anteriores.

   **Bash:**

   ```bash
   az aks create --name kubcluster \
   --resource-group sqlbdcgroup \
   --generate-ssh-keys \
   --node-vm-size Standard_L8s \
   --node-count 1 \
   --kubernetes-version <version number>
   ```

   **PowerShell:**

   ```powershell
   az aks create --name kubcluster `
   --resource-group sqlbdcgroup `
   --generate-ssh-keys `
   --node-vm-size Standard_L8s `
   --node-count 1 `
   --kubernetes-version <version number>
   ```

   Você pode aumentar ou diminuir o número de nós de agente do Kubernetes alterando o `--node-count <n>`, em que `<n>` é o número de nós de agente que você deseja usar. Isso não inclui o nó mestre do Kubernetes, que é gerenciado nos bastidores pelo AKS. O exemplo anterior usa apenas um único nó para fins de avaliação. Também é possível alterar o `--node-vm-size` para selecionar um tamanho de máquina virtual apropriado que corresponda aos seus requisitos de carga de trabalho. Use o comando `az vm list-sizes --location westus2 -o table` para listar os tamanhos disponíveis de máquinas virtuais em sua região.

   Após alguns minutos, o comando é concluído e retorna informações formatadas em JSON sobre o cluster.

   > [!TIP]
   > Se você receber erros ao criar o cluster no AKS, confira a [seção de solução de problemas](#troubleshoot) deste artigo.

1. Salve a saída JSON do comando anterior para uso posterior.

## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster

1. Para configurar o kubectl para se conectar ao cluster do Kubernetes, execute o comando [az aks get-credentials](/cli/azure/aks#az-aks-get-credentials). Esta etapa baixa as credenciais e configura a CLI do kubectl para usá-las.

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. Para verificar a conexão com o cluster, use o comando [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) para retornar uma lista dos nós de cluster.  O exemplo a seguir mostrará a saída se você tiver um mestre e três nós de agente.

   ```bash
   kubectl get nodes
   ```

## <a name="troubleshooting"></a><a id="troubleshoot"></a> Solução de problemas

Se você tiver problemas ao criar um Serviço de Kubernetes do Azure com os comandos anteriores, tente as seguintes resoluções:

- Verifique se você instalou a [CLI do Azure mais recente](/cli/azure/install-azure-cli).
- Experimente as mesmas etapas usando um grupo de recursos e um nome de cluster diferentes.
- Veja a [documentação detalhada de solução de problemas do AKS](/azure/aks/troubleshooting).

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configuraram um cluster do Kubernetes no AKS. A próxima etapa é implantar um cluster de Big Data do SQL Server 2019 no cluster do Kubernetes do AKS. Para obter mais informações sobre como implantar clusters de Big Data, confira o seguinte artigo:

[Como implantar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md)