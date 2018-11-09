---
title: Configurar o Kubernetes com kubeadm para implantações do SQL Server 2019 | Microsoft Docs
description: Saiba como configurar o Kubernetes no Ubuntu 16.04 várias ou 18.04 computadores (físicos ou virtuais) para implantações de cluster (versão prévia) do SQL Server 2019 big data.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 842a23877290aec76f7813f27b68b4bccd7b5c9b
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221772"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-2019-deployments"></a>Configurar o Kubernetes em vários computadores para implantações do SQL Server de 2019

Este artigo fornece um exemplo de como usar **kubeadm** configurar Kubernetes em vários computadores para implantações de cluster (versão prévia) do SQL Server 2019 big data. Neste exemplo, vários Ubuntu 16.04 ou 18.04 máquinas LTS (físicas ou virtuais) são o destino. Se você estiver implantando em uma plataforma diferente do Linux, você deve alterar alguns dos comandos para corresponder ao seu sistema.  

> [!TIP] 
> Para scripts de exemplo que configura o Kubernetes, consulte [criar um cluster Kubernetes usando Kubeadm no Ubuntu 16.04 LTS ou 18.04 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).

## <a name="prerequisites"></a>Prerequisites

- Várias máquinas físicas do Linux ou máquinas virtuais para usar para o cluster
- Configuração recomendada: 8 CPUs, 32 GB de memória e pelo menos de 100 GB de armazenamento para cada máquina
- Mínimo de três máquinas no cluster

## <a name="prepare-the-machines"></a>Prepare as máquinas

Em cada computador, existem vários pré-requisitos necessários. Em um terminal bash, execute os seguintes comandos em cada computador:

1. Adicionar o computador atual para o `/etc/hosts` arquivo:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Desabilite a troca em todos os dispositivos.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. Importar as chaves e registrar o repositório para o Kubernetes.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. Configure o docker e Kubernetes pré-requisitos na máquina.

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Defina `net.bridge.bridge-nf-call-iptables=1`. No Ubuntu 18.04, os comandos a seguir primeiro habilitar `br_netfilter`.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configurar o mestre de Kubernetes

Depois de executar os comandos anteriores em cada computador, escolha uma das máquinas para ser o mestre de Kubernetes. Divertidos, em seguida, os comandos a seguir no computador.

1. Primeiro, crie um arquivo rbac.yaml em seu diretório atual com o comando a seguir. 

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

1. Inicialize o mestre de Kubernetes neste computador. Você deverá ver a saída que o mestre de Kubernetes foi inicializado com êxito.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. Observação o `kubeadm join` de comando que você precisa usar nos outros servidores para ingressar no cluster Kubernetes. Copie isto para uso posterior.

   ![junção kubeadm](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Configure um arquivo de configuração do Kubernetes seu diretório base.

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
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Configurar os agentes de Kubernetes

As outras máquinas irá atuar como agentes de Kubernetes no cluster. 

Em cada um dos outros computadores, execute o `kubeadm join` comando que você copiou na seção anterior.

![agentes de junção kubeadm](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Exibir o status do cluster

Para verificar a conexão ao seu cluster, use o [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) comando para retornar uma lista de nós do cluster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configurado um cluster Kubernetes em vários computadores Ubuntu. A próxima etapa é implantar um cluster de big data do SQL Server 2019. Para obter instruções, consulte o artigo a seguir:

[Implantar o SQL Server de 2019 CTP 2.1 no Kubernetes](deployment-guidance.md#deploy)
