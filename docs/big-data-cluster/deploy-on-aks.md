---
title: Configurar o serviço de Kubernetes do Azure
titleSuffix: SQL Server big data clusters
description: Saiba como configurar o serviço de Kubernetes do Azure (AKS) para implantações de cluster (versão prévia) do SQL Server 2019 big data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/10/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d39f62345a539094c585b196c9b6030b673f8e89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958482"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>Configurar o serviço Kubernetes do Azure para implantações de cluster de big data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como configurar o serviço de Kubernetes do Azure (AKS) para implantações de cluster (versão prévia) do SQL Server 2019 big data.

AKS torna simples a criar, configurar e gerenciar um cluster de máquinas virtuais que são pré-configuradas com um cluster Kubernetes para executar aplicativos em contêineres. Isso permite que você use suas habilidades existentes ou explore um grande e crescente Conhecimento da comunidade, para implantar e gerenciar aplicativos baseados em contêiner no Microsoft Azure.

Este artigo descreve as etapas para implantar o Kubernetes no AKS usando a CLI do Azure. Se você não tiver uma assinatura do Azure, crie uma conta gratuita, antes de começar.

> [!TIP] 
> Para um script de python de exemplo que implanta o cluster de big data do AKS e o SQL Server, consulte [guia de início rápido: Implantar o SQL Server no serviço de Kubernetes do Azure (AKS) de cluster de big data](quickstart-big-data-cluster-deploy.md).

## <a name="prerequisites"></a>Pré-requisitos

- [Implantar as ferramentas de big data do SQL Server 2019](deploy-big-data-tools.md):
   - **Kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **CLI do Azure**

- Versão mínima 1.10 para o servidor de Kubernetes. Para o AKS, você precisará usar `--kubernetes-version` parâmetro para especificar uma versão diferente do padrão.

- Para obter uma experiência ideal ao validar cenários básicos de AKS, use:
   - 8 vCPUs em todos os nós
   - 32 GB de memória por VM
   - 24 ou anexados mais discos em todos os nós

   > [!TIP]
   > Infraestrutura do Azure oferece várias opções de tamanho para VMs, consulte [aqui](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) para seleções na região em que você planeja implantar.

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Um grupo de recursos do Azure é um grupo lógico no qual Azure recursos são implantados e gerenciados. As etapas a seguir entrar no Azure e criar um grupo de recursos para o cluster do AKS.

1. No prompt de comando, execute o seguinte comando e siga os prompts para fazer logon em sua assinatura do Azure:

    ```azurecli
    az login
    ```

1. Se você tiver várias assinaturas, você pode exibir todas as suas assinaturas, executando o seguinte comando:

   ```azurecli
   az account list
   ```

1. Se você quiser alterar para uma assinatura diferente, você pode executar este comando:

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. Criar um grupo de recursos com o **criar grupo de az** comando. O exemplo a seguir cria um grupo de recursos denominado `sqlbdcgroup` no `westus2` local.

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>Verifique se as versões disponíveis do Kubernetes

Use a versão mais recente disponível do Kubernetes. A versão mais recente disponível depende do local em que você está implantando o cluster. O comando a seguir retorna as versões do Kubernetes disponíveis em um local específico.

Antes de executar o comando, atualize o script. Substitua `<Azure data center>` com o local do seu cluster.

   **bash**

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

Escolha a versão mais recente disponível para seu cluster. Registre o número de versão. Você o usará na próxima etapa.

## <a name="create-a-kubernetes-cluster"></a>Criar um cluster Kubernetes

1. Criar um cluster Kubernetes no AKS com o [criar az aks](https://docs.microsoft.com/cli/azure/aks) comando. O exemplo a seguir cria um cluster Kubernetes chamado *kubcluster* com um nó de agente do Linux de tamanho **Standard_L8s**.

   Antes de executar o script, substitua `<version number>` com o número de versão que você identificou na etapa anterior.

   Certifique-se de que criar o cluster do AKS no mesmo grupo de recursos que você usou nas seções anteriores.

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

   Você pode aumentar ou diminuir o número de nós de agente do Kubernetes, alterando a `--node-count <n>` onde `<n>` é o número de nós de agente que você deseja usar. Isso não inclui o nó mestre do Kubernetes, que é gerenciado pelo AKS em segundo plano. O exemplo anterior usa apenas um único nó para fins de avaliação.

   Após alguns minutos, o comando for concluído e retorna informações formatadas em JSON sobre o cluster.

   > [!TIP]
   > Se você receber erros ao criar o cluster no AKS, consulte o [seção solução de problemas](#troubleshoot) deste artigo.

1. Salve a saída JSON do comando anterior para uso posterior.

## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster

1. Para configurar o kubectil para conectar-se ao cluster Kubernetes, execute as [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando. Esta etapa baixa credenciais e configura o kubectl CLI para usá-los.

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. Para verificar a conexão ao seu cluster, use o [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) comando para retornar uma lista de nós do cluster.  O exemplo a seguir mostra a saída se você tem 1 mestre e nós de agente 3.

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> Solução de problemas

Se você tiver problemas ao criar um serviço de Kubernetes do Azure com os comandos anteriores, tente as seguintes resoluções:

- Certifique-se de que você instalou o [CLI do Azure mais recente](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).
- Tente as mesmas etapas usando um nome de cluster e do grupo de recursos diferente.

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configurado um cluster Kubernetes no AKS. A próxima etapa é implantar um cluster de big data 2019 do SQL Server no cluster AKS Kubernetes. Para obter mais informações sobre como implantar clusters de big data, consulte o artigo a seguir:

[Como implantar clusters de grandes dados do SQL Server no Kubernetes](deployment-guidance.md)
