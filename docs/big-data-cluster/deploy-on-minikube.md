---
title: Configurar o minikube
titleSuffix: SQL Server big data clusters
description: Saiba como configurar o minikube para implantações de cluster de Big Data do SQL Server 2019 (versão prévia) em um único computador.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c2261b5cfbbe590c76ce410da4b95ee678a20b5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958471"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>Configurar o minikube para implantações de cluster de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como configurar o **minikube** em um único computador para implantações de cluster de Big Data do SQL Server 2019 (versão prévia). Minikube é uma ferramenta que facilita a execução de Kubernetes em um único computador, como um laptop ou um desktop. O minikube executa um cluster do Kubernetes de nó único dentro de uma VM em seu laptop para os usuários que desejam experimentar o Kubernetes ou desenvolver com ele no dia a dia. 

## <a name="prerequisites"></a>Prerequisites

- 32 GB de memória (recomendado de 64 GB).

- Se o computador tiver apenas a memória mínima recomendada, configure a implantação do cluster para ter apenas uma instância do pool de computação, uma instância do pool de dados e uma instância do pool de armazenamento. Essa configuração deve ser usada somente para ambientes de avaliação em que a durabilidade e a disponibilidade dos dados não são importantes. Confira a [documentação de implantação](deployment-guidance.md#configfile) para obter mais informações sobre as variáveis de ambiente a serem definidas para configurar o número de réplicas para pools de dados, pools de computação e pools de armazenamento.

- A virtualização VT-x ou AMD-v deve estar habilitada no BIOS do computador.

## <a name="install-dependencies"></a>Instalar dependências

1. Instale o [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Instale o Python 3:
   - Se pip estiver ausente, baixe [get-clspip.py](https://bootstrap.pypa.io/get-pip.py) e execute `python get-pip.py`.
   - Instale o pacote de solicitações usando `python -m pip install requests`.

1. Se você ainda não tiver um hipervisor instalado, instale um agora.
   - No OS X, instale [xhyve driver](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) ou [VMware Fusion](https://www.vmware.com/products/fusion).
   - No Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) ou [KVM](https://www.linux-kvm.org/).
   - No Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) ou [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Se você não tiver um comutador externo configurado no Hyper-v, crie um que tenha acesso à rede externa.  Confira como [criar um comutador externo no Hyper-v para o minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalar o minikube

Instale o minikube de acordo com as instruções para a [versão v0.28.2](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). O cluster de Big Data do SQL Server 2019 (versão prévia) funciona apenas com a versão v0.24.1 e superior.

## <a name="create-a-minikube-cluster"></a>Criar um cluster do minikube

O comando a seguir cria um cluster do minikube em uma VM do Hyper-V com 8 CPUs, 28 GB de memória e tamanho de disco de 100 GB. O tamanho do disco não é espaço reservado.  Ele aumenta para esse tamanho em disco, conforme necessário.  É recomendável não alterar o espaço em disco para algo inferior a 100 GB, pois encontramos problemas com isso no teste. Isso também especifica o comutador do Hyper-v com acesso externo explicitamente.

Altere os parâmetros, como **--memory**, conforme necessário, dependendo do hardware disponível e do hipervisor que você está usando.  Verifique se o valor do parâmetro de comutador virtual **--hyper-v** corresponde ao nome usado ao criar o comutador virtual.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

Se você estiver usando o minikube com VirtualBox, o comando ficará assim:

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Desabilitar o ponto de verificação automático com o Hyper-V

No Windows 10, o ponto de verificação automático é habilitado em uma VM. Execute o comando a seguir no PowerShell para desabilitar o ponto de verificação automático na VM.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>Próximas etapas

As etapas neste artigo configuraram um cluster do minikube. A próxima etapa é implantar o cluster de Big Data do SQL Server 2019. Para obter instruções, confira o seguinte artigo:

[Implantar clusters de Big Data do SQL Server 2019 no Kubernetes](deployment-guidance.md#deploy)
