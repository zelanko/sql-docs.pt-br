---
title: Configurar o Kubernetes com kubeadm
titleSuffix: SQL Server Big Data Clusters
description: Saiba como configurar o Kubernetes em vários computadores com Ubuntu 16.04 ou 18.04 (físicos ou virtuais) para implantações do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6b5f2c8dac062f147326a0b9fcfb7120f0648729
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74165431"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>Configurar o Kubernetes em vários computadores para implantações de cluster de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece um exemplo de como usar **kubeadm** para configurar o Kubernetes em vários computadores para implantações do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Neste exemplo, vários computadores com Ubuntu 16.04 ou 18.04 LTS (físicos ou virtuais) são o destino. Se você estiver implantando em uma plataforma diferente do Linux, deverá alterar alguns dos comandos para corresponder ao seu sistema.  

> [!TIP] 
> Para scripts de exemplo que configuram o Kubernetes, consulte [Criar um cluster do Kubernetes usando Kubeadm no Ubuntu 16.04 LTS ou 18.04 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).
Além disso, consulte [este](deployment-script-single-node-kubeadm.md) tópico para ver um script de exemplo que automatiza uma implantação de uma única implantação de kubeadm de nó único em uma VM e implanta uma configuração padrão de cluster de Big Data sobre ela.

## <a name="prerequisites"></a>Prerequisites

- Mínimo de três computadores físicos ou máquinas virtuais com Linux
- Configuração recomendada por computador:
   - 8 CPUs
   - 64 GB de memória
   - 100 GB de armazenamento
 
> [!Important] 
> Antes de iniciar a implantação do cluster de Big Data, verifique se os relógios estão sincronizados em todos os nós do Kubernetes que serão destinos da implantação. Como o cluster de Big Data tem propriedades de integridade internas para vários serviços que são sensíveis ao tempo, distorções de relógio podem causar status incorretos.

## <a name="prepare-the-machines"></a>Preparar os computadores

Em cada computador, há vários pré-requisitos necessários. Em um terminal de Bash, execute os seguintes comandos em cada computador:

1. Adicione o computador atual ao arquivo `/etc/hosts`:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Desabilite a troca em todos os dispositivos.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. Importe as chaves e registre o repositório para o Kubernetes.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. Configure os pré-requisitos do Docker e do Kubernetes no computador.

   ```bash
   KUBE_DPKG_VERSION=1.15.0-00 #or your other target K8s version, which should be at least 1.13.
   sudo apt-get update && \
   sudo apt-get install -y ebtables ethtool && \
   sudo apt-get install -y docker.io && \
   sudo apt-get install -y apt-transport-https && \
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && \
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Defina `net.bridge.bridge-nf-call-iptables=1`. No Ubuntu 18.04, os comandos a seguir habilitam o `br_netfilter` primeiro.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configurar o Kubernetes mestre

Depois de executar os comandos anteriores em cada computador, escolha um dos computadores para ser o Kubernetes mestre. Em seguida, execute os seguintes comandos nesse computador.

1. Primeiro, crie um arquivo rbac.yaml no diretório atual com o comando a seguir. 

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

1. Inicialize o Kubernetes mestre nesse computador. O script de exemplo abaixo especifica a versão `1.15.0` do Kubernetes. A versão usada depende do cluster do Kubernetes.

   ```bash
   KUBE_VERSION=1.15.0
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

   Você deve ver a saída que o Kubernetes mestre foi inicializado com êxito.

1. Observe o comando `kubeadm join` que você precisa usar nos outros servidores para unir o cluster do Kubernetes. Copie isso para uso posterior.

   ![kubeadm join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Configure um arquivo de configuração do Kubernetes em seu diretório base.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. Configure o cluster e o painel do Kubernetes.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Configurar os agentes do Kubernetes

Os outros computadores atuarão como agentes do Kubernetes no cluster. 

Em cada um dos outros computadores, execute o comando `kubeadm join` que você copiou na seção anterior.

![kubeadm join agents](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Exibir o status do cluster

Para verificar a conexão com o cluster, use o comando [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) para retornar uma lista dos nós de cluster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configuraram um cluster do Kubernetes em vários computadores Ubuntu. A próxima etapa é implantar o cluster de Big Data do SQL Server 2019. Para obter instruções, confira o seguinte artigo:

[Implantar o SQL Server no Kubernetes](deployment-guidance.md#deploy)
