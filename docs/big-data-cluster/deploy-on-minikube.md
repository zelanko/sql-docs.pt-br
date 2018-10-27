---
title: Configurar o Minikube para implantações de cluster do SQL Server 2019 big data | Microsoft Docs
description: Saiba como configurar o Minikube para implantações de cluster (versão prévia) de big data de 2019 do SQL Server em um único computador.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 71523efb55fd1bc41927b38d2e91abc9833c73b0
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050778"
---
# <a name="configure-minikube-for-sql-server-2019-big-data-cluster-deployments"></a>Configurar o Minikube para implantações de cluster do SQL Server 2019 big data

Este artigo descreve como configurar **minikube** em um único computador para implantações de cluster (versão prévia) do SQL Server 2019 big data. Minikube é uma ferramenta que torna mais fácil de executar Kubernetes em um único computador, como um laptop ou desktop. Minikube executa um cluster do Kubernetes de nó único dentro de uma VM em seu laptop para usuários que desejam experimentar Kubernetes ou desenvolver com ele diárias. 

## <a name="prerequisites"></a>Prerequisites

- Para executar um cluster Minikube para SQL Server 2019 CTP 2.0 em uma configuração de cluster de big data do SQL, é recomendável que seu computador tenha pelo menos 32 GB de RAM.

   > [!TIP] 
   > Se o computador tem apenas o mínimo recomendado de memória, em seguida, configure a implantação do cluster para ter apenas 1 instância de pool de computação, 1 instância de pool de dados e instância de pool de armazenamento de 1. Essa configuração só deve ser usada para ambientes de avaliação em que a durabilidade e disponibilidade dos dados são importantes. Consulte a [documentação de implantação](deployment-guidance.md#define-environment-variables) para obter mais informações sobre as variáveis de ambiente para configurar o número de réplicas para pools de dados, computação pools e pools de armazenamento.

- Virtualização x VT ou AMD-v deve ser habilitada no BIOS do computador.

## <a name="install-dependencies"></a>Instale as dependências

1. Se não estiver instalado, instale o git localmente no [Windows](https://git-for-windows.github.io/), [Linux ou Mac](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

1. Instale [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Instale o Python 3:
   - Se o pip está ausente, baixe [get-clspip.py](https://bootstrap.pypa.io/get-pip.py) e execute `python get-pip.py`.
   - Solicitações de instalação de pacote usando `python -m pip install requests`.

1. Se você ainda não tiver um hipervisor instalado, instale um agora.
   - Para OS X, instale [driver xhyve](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads), ou [VMware Fusion](https://www.vmware.com/products/fusion).
   - Para o Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) ou [KVM](http://www.linux-kvm.org/).
   - Para Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) ou [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Se você não tiver um comutador externo configurado no hyper-v, em seguida, crie um que tenha acesso à rede externa.  Veja como [criar um comutador externo no hyper-v para minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalar o Minikube

Instalar o Minikube acordo com as instruções para o [v0.28.2 versão](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). O cluster de big data do SQL Server de 2019 CTP 2.0 funciona somente com a versão v0.24.1 e backup.

## <a name="create-a-minikube-cluster"></a>Criar um cluster do Minikube

O comando a seguir cria um cluster do minikube em uma VM do Hyper-V com 8 CPUs, 28 GB de memória e o tamanho do disco de 100 GB. O tamanho do disco não é um espaço reservado.  Ele cresce para que o tamanho em disco conforme necessário.  É recomendável não alterar o disco de espaço para algo menos de 100 GB tivemos problemas com isso no teste. Isso também especifica o comutador do hyper-v com acesso externo explicitamente.

Alterar os parâmetros, como **– memória** conforme necessário, dependendo de seu hardware disponível e que hipervisor que você está usando.  Verifique se o **– hyper-v** valor do parâmetro de comutador virtual corresponde ao nome que você usou ao criar o comutador virtual.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

Se você estiver usando o Minikube com o VirtualBox, o comando teria esta aparência:

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Desabilitar ponto de verificação automático com o Hyper-V

No Windows 10, o ponto de verificação automático está habilitado em uma máquina virtual. Execute o comando a seguir no PowerShell para desabilitar o ponto de verificação automático na VM.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configurado um cluster Minikube. A próxima etapa é implantar um cluster de big data do SQL Server 2019. Para obter instruções, consulte o artigo a seguir:

[Implantar o SQL Server de 2019 CTP 2.0 em Kubernetes](deployment-guidance.md#deploy)
