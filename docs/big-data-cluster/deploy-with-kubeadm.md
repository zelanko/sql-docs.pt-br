---
title: Configurar o kubernetes com kubeadm
titleSuffix: SQL Server big data clusters
description: Saiba como configurar o kubernetes em vários computadores Ubuntu 16, 4 ou 18, 4 (físico ou virtual) para implantações SQL Server 2019 Big Data cluster (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea79503869e7d403e4d3f4f960de9c95760eda0f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419450"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>Configurar o kubernetes em vários computadores para implantações de cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece um exemplo de como usar o **kubeadm** para configurar o kubernetes em vários computadores para implantações SQL Server 2019 Big data cluster (versão prévia). Neste exemplo, vários computadores Ubuntu 16, 4 ou 18, 4 LTS (físico ou virtual) são o destino. Se você estiver implantando em uma plataforma diferente do Linux, deverá alterar alguns dos comandos para corresponder ao seu sistema.  

> [!TIP] 
> Para scripts de exemplo que configuram o kubernetes, consulte [criar um cluster kubernetes usando Kubeadm no Ubuntu 16, 4 LTS ou 18, 4 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).

## <a name="prerequisites"></a>Pré-requisitos

- Mínimo de três máquinas físicas ou máquinas virtuais do Linux
- Configuração recomendada por computador:
   - 8 CPUs
   - 64 GB de memória
   - 100 GB de armazenamento

## <a name="prepare-the-machines"></a>Preparar os computadores

Em cada máquina, há vários pré-requisitos necessários. Em um terminal Bash, execute os seguintes comandos em cada computador:

1. Adicione o computador atual ao `/etc/hosts` arquivo:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Desabilite a permuta em todos os dispositivos.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. Importe as chaves e registre o repositório para kubernetes.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. Configure os pré-requisitos do Docker e do kubernetes no computador.

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Defina `net.bridge.bridge-nf-call-iptables=1`. No Ubuntu 18, 4, os comandos a seguir habilitam `br_netfilter`primeiro.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configurar o mestre kubernetes

Depois de executar os comandos anteriores em cada computador, escolha uma das máquinas para ser o mestre do kubernetes. Em seguida, execute os comandos a seguir nesse computador.

1. Primeiro, crie um arquivo RBAC. YAML no diretório atual com o comando a seguir. 

   ```bash
   cat <<EOF > rbac.yaml
   apiVersion: rbac.authorization.k8s.io/v1beta1
   kind: ClusterRoleBinding
   metadata:
     name: default-rbac
   subjects:
   - kind: ServiceAccount
     name: default
     namespace: default
   roleRef:
     kind: ClusterRole
     name: cluster-admin
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. Inicialize o mestre kubernetes neste computador. Você deve ver a saída de que o mestre kubernetes foi inicializado com êxito.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. Observe o `kubeadm join` comando que você precisa usar nos outros servidores para ingressar no cluster kubernetes. Copie isso para uso posterior.

   ![kubeadm Join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Configure um arquivo de configuração do kubernetes seu diretório base.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. Configure o cluster e o painel do kubernetes.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Configurar os agentes kubernetes

Os outros computadores atuarão como agentes kubernetes no cluster. 

Em cada uma das outras máquinas, execute o `kubeadm join` comando que você copiou na seção anterior.

![agentes de junção do kubeadm](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Exibir o status do cluster

Para verificar a conexão com o cluster, use o comando [kubectl Get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) para retornar uma lista de nós de cluster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configuraram um cluster kubernetes em vários computadores Ubuntu. A próxima etapa é implantar SQL Server 2019 Big Data cluster. Para obter instruções, consulte o seguinte artigo:

[Implantar SQL Server em kubernetes](deployment-guidance.md#deploy)
