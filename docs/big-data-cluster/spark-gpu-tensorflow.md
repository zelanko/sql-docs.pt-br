---
title: Suporte de GPU e TensorFlow
titleSuffix: SQL Server big data clusters
description: Implantar um cluster de big data com suporte GPU e usar o TensorFlow em blocos de anotações do Azure Data Studio.
author: inchiosa
ms.author: marinch
ms.reviewer: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2d31736ee4dd68857e3afce678b6dd806701a82b
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774946"
---
# <a name="deploy-a-big-data-cluster-with-gpu-support-and-run-tensorflow"></a>Implantar um cluster de big data com suporte GPU e executar o TensorFlow

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo demonstra como implantar um cluster de big data no Azure Kubernetes AKS (serviço) que dá suporte a pools de nós habilitadas para GPU para cargas de trabalho de computação intensiva. Assim, você pode executar blocos de anotações de exemplo no Studio de dados do Azure que realizar a classificação de imagem com o TensorFlow para GPU.

## <a name="prerequisites"></a>Prerequisites

- [Ferramentas de big data](deploy-big-data-tools.md):
  - **mssqlctl**
  - **kubectl**
  - **Azure Data Studio**
  - **Extensão do SQL Server de 2019**
  - **CLI do Azure**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="create-an-aks-cluster"></a>Criar um cluster AKS

As etapas a seguir usam a CLI do Azure para criar um cluster do AKS que dá suporte a GPUs.

1. No prompt de comando, execute o seguinte comando e siga os prompts para fazer logon em sua assinatura do Azure:

    ```azurecli
    az login
    ```

1. Criar um grupo de recursos com o **criar grupo de az** comando. O exemplo a seguir cria um grupo de recursos denominado `sqlbigdatagroupgpu` no `eastus` local.

   ```azurecli
   az group create --name sqlbigdatagroupgpu --location eastus
   ```

1. Criar um cluster Kubernetes no AKS com o [criar az aks](https://docs.microsoft.com/cli/azure/aks) comando. O exemplo a seguir cria um cluster Kubernetes chamado `gpucluster` no `sqlbigdatagroupgpu` grupo de recursos.

   ```azurecli
   az aks create --name gpucluster --resource-group sqlbigdatagroupgpu --generate-ssh-keys --node-vm-size Standard_NC6s_v3 --node-count 3 --node-osdisk-size 50 --kubernetes-version 1.11.9 --location eastus
   ```

   > [!NOTE]
   > Este cluster usa o **Standard_NC6s_v3** [tamanho da máquina de virtual otimizados para GPU](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-gpu), que é uma das máquinas virtuais especializadas disponíveis com o único ou vários GPUs NVIDIA. Para obter mais informações, consulte [GPUs de uso para cargas de trabalho de computação intensa no serviço de Kubernetes do Azure (AKS)](https://docs.microsoft.com/azure/aks/gpu-cluster).

1. Para configurar o kubectil para conectar-se ao cluster Kubernetes, execute as [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando.

   ```azurecli
   az aks get-credentials --overwrite-existing --resource-group=sqlbigdatagroupgpu --name gpucluster
   ```

## <a name="apply-yaml-manifest"></a>Aplicar o manifesto YAML

1. Use **kubectl** para criar um namespace de Kubernetes chamado `gpu-resources`.

   ```bash
   kubectl create namespace gpu-resources
   ```

1. Salvar o conteúdo do arquivo YAML a seguir em um arquivo chamado **nvidia-dispositivo-plugin-ds.yaml**. Salvá-lo para o diretório de trabalho em seu computador que você está executando **kubectl** do.

   Atualização de `image: nvidia/k8s-device-plugin:1.11` meio para baixo o manifesto para corresponder à sua versão do Kubernetes. Por exemplo, se o cluster do AKS executar Kubernetes versão 1.12, atualize a marca a `image: nvidia/k8s-device-plugin:1.12`.

   ```yaml
   apiVersion: extensions/v1beta1
   kind: DaemonSet
   metadata:
     labels:
       kubernetes.io/cluster-service: "true"
     name: nvidia-device-plugin
     namespace: gpu-resources
   spec:
     template:
       metadata:
         # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler
         # reserves resources for critical add-on pods so that they can be rescheduled after
         # a failure.  This annotation works in tandem with the toleration below.
         annotations:
           scheduler.alpha.kubernetes.io/critical-pod: ""
         labels:
           name: nvidia-device-plugin-ds
       spec:
         tolerations:
         # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode.
         # This, along with the annotation above marks this pod as a critical add-on.
         - key: CriticalAddonsOnly
           operator: Exists
         containers:
         - image: nvidia/k8s-device-plugin:1.11 # Update this tag to match your Kubernetes version
           name: nvidia-device-plugin-ctr
           securityContext:
             allowPrivilegeEscalation: false
             capabilities:
               drop: ["ALL"]
           volumeMounts:
             - name: device-plugin
               mountPath: /var/lib/kubelet/device-plugins
         volumes:
           - name: device-plugin
             hostPath:
               path: /var/lib/kubelet/device-plugins
         nodeSelector:
           beta.kubernetes.io/os: linux
           accelerator: nvidia
   ```

1. Enquanto, use o kubectl aplicar o comando para criar o DaemonSet. **NVIDIA-dispositivo-plugin-ds.yaml** deve estar no diretório de trabalho quando você executar o comando a seguir:

   ```bash
   kubectl apply -f nvidia-device-plugin-ds.yaml
   ```

## <a name="deploy-the-big-data-cluster"></a>Implantar o cluster de big data

Para implantar um cluster de big data de 2019 do SQL Server (versão prévia) que dá suporte a GPUs, você deve implantar de um registro de docker específico e o repositório. As seguintes variáveis de ambiente são diferentes para uma implantação de GPU:

| Variável de ambiente | Valor |
|---|---|
| **DOCKER_REGISTRY** | `marinchcreus3.azurecr.io` |
| **DOCKER_REPOSITORY** | `ctp25-8-0-61-gpu` |
| **DOCKER_USERNAME** | `<your username, gpu-specific credentials provided by Microsoft>` |
| **DOCKER_PASSWORD** | `<your password, gpu-specific credentials provided by Microsoft>` |

Use **mssqlctl** para implantar o cluster, selecione a configuração do aks-dev-test.json e fonte personalizado valores acima, quando solicitado.

```bash
mssqlctl cluster create
```

> [!TIP]
> O nome padrão do cluster de big data é `mssql-cluster`.

Você também pode personalizar ainda mais sua implantação, passando um arquivo de configuração de implantação personalizada. Para obter mais informações, consulte o [diretrizes de implantação](deployment-guidance.md#customconfig).

## <a name="run-the-tensorflow-example"></a>Executar o exemplo de TensorFlow

Os seguintes blocos de anotações de dois exemplo demonstram aos modelos de classificação duas imagens de treinamento em um único nó do cluster Spark usando TensorFlow para GPU.

| Download do bloco de anotações | Descrição |
|---|---|
| [**tf-cuda8.ipynb**](https://aka.ms/AA4jdgd) | Usa 8 de CUDA, CUDNN 6 e TensorFlow 1.4.0.  |
| [**tf-cuda9.ipynb**](https://aka.ms/AA4ixzr) | Usa CUDA 9 e CUDNN 7 TensorFlow 1.12.0. |

Coloque o arquivo de notebook apropriado para seu computador local e, em seguida, abrir e executá-lo no estúdio de dados do Azure usando o kernel PySpark3. A menos que você tenha uma necessidade específica para uma versão mais antiga do CUDA ou o TensorFlow, escolha CUDA 9/CUDNN 7/TensorFlow 1.12.0. Para obter mais informações sobre como usar blocos de anotações com clusters de big data, consulte [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).

> [!NOTE]
> Observe que os blocos de anotações, instalar software em locais de sistema. Isso é possível porque os blocos de anotações, atualmente, executam com privilégios de raiz no CTP 2.5.

Depois de instalar o TensorFlow e bibliotecas de GPU NVIDIA GPU, os blocos de anotações listam dispositivos GPU disponíveis. Em seguida, eles se ajustar e avaliar um modelo do TensorFlow para reconhecer usando o conjunto de dados MNIST de dígitos manuscritos. Depois de verificar o espaço em disco disponível, baixe e execute o exemplo de classificação de imagens CIFAR 10 da [ https://github.com/tensorflow/models.git ](https://github.com/tensorflow/models.git). Ao executar o exemplo de CIFAR 10 em clusters que tenham GPUs diferentes, você pode observar o aumento de velocidade oferecidas por cada geração de GPU disponível no Azure.

## <a name="clean-up-resources"></a>Limpar recursos

Para excluir o cluster de big data, use o seguinte comando:

```bash
mssqlctl cluster delete --name gpubigdatacluster
```

O comando anterior não remove o cluster do AKS. Para excluir o cluster do AKS e os recursos associados a ele, use o seguinte comando:

```azurecli
az group delete -n sqlbigdatagroupgpu
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server (versão prévia), consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
