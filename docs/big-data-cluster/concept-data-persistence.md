---
title: Persistência de dados com o SQL Server, o cluster de big data no Kubernetes | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 629d7fd887e96013b17a5686ce82eb966044f240
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795853"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistência de dados com o cluster de big data do SQL Server no Kubernetes

[Volumes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) fornecem um modelo de plug-in para armazenamento no Kubernetes como o armazenamento é fornecido em que é concluído, abstraído do como eles são consumidos. Você pode, portanto, traga seu próprio armazenamento altamente disponível e conectá-lo ao cluster do cluster de big data do SQL Server. Isso lhe dá controle total sobre o tipo de armazenamento, disponibilidade e desempenho que você precisa. Kubernetes dá suporte a vários tipos de soluções de armazenamento, incluindo discos/arquivos do Azure, NFS, armazenamento local e muito mais.

## <a name="configure-persistent-volumes"></a>Configurar volumes persistentes

A maneira de cluster de big data do SQL Server consome esses volumes persistentes é por meio [Classes de armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Você pode criar classes de armazenamento diferentes para diferentes tipos de armazenamento e especificá-los no momento da implantação de cluster de big data. Você pode configurar qual classe de armazenamento a ser usado para qual finalidade (pool). Cluster de big data do SQL Server cria [declarações de volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) com o nome de classe de armazenamento especificado para cada pod que requer volumes persistentes. Ele, em seguida, monta os volumes persistentes correspondentes no pod.

> [!NOTE]
> Para o CTP 2.0, apenas `ReadWriteOnce` é suporte para o modo de acesso para o cluster inteiro.

## <a name="deployment-settings"></a>Configurações de implantação

Para usar o armazenamento persistente durante a implantação, configure a **USE_PERSISTENT_VOLUME** e **STORAGE_CLASS_NAME** variáveis de ambiente antes de executar `mssqlctl create cluster` comando. **USE_PERSISTENT_VOLUME** é definido como `true` por padrão. Você pode substituir o padrão e defina-o como `false` e, nesse caso, o cluster de big data do SQL Server usa emptyDir montagens. 

> [!WARNING]
> A execução sem armazenamento persistente pode resultar em um cluster não funcional. Após a reinicialização de pod, dados de metadados e/ou usuário do cluster serão perdidos permanentemente.

Se você definir o sinalizador como true, você também deve fornecer **STORAGE_CLASS_NAME** como um parâmetro no momento da implantação.

## <a name="aks-storage-classes"></a>Classes de armazenamento do AKS

Acompanha o AKS [duas classes de armazenamento interno](https://docs.microsoft.com/en-us/azure/aks/azure-disks-dynamic-pv) **padrão** e **o armazenamento premium** juntamente com provisionador dinâmico para eles. Você pode especificar qualquer uma dessas ou criar sua própria classe de armazenamento para a implantação de cluster de big data com o armazenamento persistente habilitado.

## <a name="minikube-storage-class"></a>Classe de armazenamento do Minikube

Minikube vem com uma classe de armazenamento interna chamada **standard** junto com um provedor dinâmico para ele.

## <a name="kubeadm"></a>Kubeadm

Kubeadm não vem com uma classe de armazenamento interno; Portanto, nós criamos scripts para configurar volumes persistentes e classes de armazenamento usando o armazenamento local ou [torre](https://github.com/rook/rook) armazenamento.

## <a name="on-premises-cluster"></a>Cluster local

Clusters locais, obviamente, não vêm com qualquer classe de armazenamento interno, portanto você deve configurar [volumes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)/[provisionadores](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/) antecipadamente e, em seguida, usar correspondente classes de armazenamento durante a implantação de cluster de big data do SQL Server.

# <a name="customize-storage-size-for-each-pool"></a>Personalizar o tamanho de cada pool de armazenamento
Por padrão, o tamanho do volume persistente provisionado para cada um dos pods provisionados no cluster é 6 GB. Isso é configurável, definindo a variável de ambiente `STORAGE_SIZE` para um valor diferente. Por exemplo, você pode executar comando abaixo para definir o valor como 10 GB, antes de executar o `mssqlctl create cluster command`.

```bash
export STORAGE_SIZE=10Gi
```

Você também pode ter configurações diferentes para configurações de armazenamento persistente, esse nome de classe de armazenamento e tamanhos de volume persistente para pools diferentes no cluster. Por exemplo, você pode configurar os volumes persistentes implantados para o pool de armazenamento para usar uma classe de armazenamento diferentes e ter maior capacidade pela configuração abaixo das variáveis de ambiente antes de implantar o cluster:

```bash
export STORAGE_POOL_USE_PERSISTENT_VOLUME=true
export STORAGE_POOL_STORAGE_CLASS_NAME=premium-storage
export STORAGE_POOL_STORAGE_SIZE=100Gi
```

Aqui está uma lista abrangente das variáveis de ambiente relacionados à configuração de armazenamento persistente para o cluster de Big Data do SQL Server:

| Variável de ambiente | Valor padrão | Description |
|---|---|---|
| **USE_PERSISTENT_VOLUME** | true | `true` Para usar declarações de Volume persistente Kubernetes para o armazenamento de pod. `false` Para usar o armazenamento efêmero host para o armazenamento de pod. |
| **STORAGE_CLASS_NAME** | padrão | Se `USE_PERSISTENT_VOLUME` é `true` isso indica o nome de classe de armazenamento Kubernetes para usar. |
| **STORAGE_SIZE** | Gi 6 | Se `USE_PERSISTENT_VOLUME` é `true`, isso indica que o tamanho do volume persistente para cada pod. |
| **DATA_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Para usar declarações de Volume persistente Kubernetes para pods no pool de dados. `false` Para usar o armazenamento efêmero host para pods de pool de dados. |
| **DATA_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | Indica o nome da classe de armazenamento Kubernetes a ser usado para volumes persistentes associados pods de pool de dados.|
| **DATA_POOL_STORAGE_SIZE** | STORAGE_SIZE |Indica o tamanho de volume persistente para cada pod no pool de dados. |
| **STORAGE_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Para usar declarações de Volume persistente Kubernetes para pods no pool de armazenamento. `false` Para usar o armazenamento efêmero host para pods de pool de armazenamento.|
| **STORAGE_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | TIndicates o nome da classe de armazenamento Kubernetes a ser usado para volumes persistentes associados pods de pool de armazenamento. |
| **STORAGE_POOL_STORAGE_SIZE** | STORAGE_SIZE | Indica o tamanho de volume persistente para cada pod no pool de armazenamento. |

## <a name="next-steps"></a>Próximas etapas

Para obter a documentação completa sobre os volumes no Kubernetes, consulte o [documentação do Kubernetes em Volumes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obter mais informações sobre como implantar o cluster de big data do SQL Server, consulte [como implantar o SQL Server, o cluster de big data no Kubernetes](deployment-guidance.md).

