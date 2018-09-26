---
title: Gerenciar um grupo de disponibilidade SQL Server Always On Kubernetes
description: Este artigo explica como gerenciar um SQL Server sempre no grupo de disponibilidade no Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 078149ff8d9c9c81ac8db95862bf685ca66fbe36
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049346"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Gerenciar o SQL Server Always On Kubernetes do grupo de disponibilidade

Para gerenciar um grupo de disponibilidade AlwaysOn no Kubernetes, crie um manifesto e aplicá-lo ao cluster. O manifesto é um `.yaml` arquivo.  

Os exemplos neste artigo se aplicam a todos os cluster de Kubernetes. Os cenários nesses exemplos são aplicados em relação a um cluster no serviço Kubernetes do Azure.

Veja um exemplo de como da implantação de ponta a ponta no [este tutorial](tutorial-sql-server-ag-kubernetes.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Failover - grupo de disponibilidade do SQL Server no Kubernetes

Para fazer failover de uma réplica primária do grupo de disponibilidade para um nó diferente no Kubernetes, use um trabalho. Este artigo identifica as variáveis de ambiente para esse trabalho.

O exemplo a seguir de um arquivo de manifesto descreve um trabalho para o failover manualmente de trabalho para um grupo de disponibilidade em uma réplica de Kubernetes. Copie o conteúdo do exemplo em um novo arquivo chamado `failover.yaml`.

[failover.YAML](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates/failover.yaml)

Para implantar o trabalho, use `Kubectl`.

```azurecli
kubectl apply -f failover.yaml
```

Quando você aplica o arquivo de manifesto, o Kubernetes executa o trabalho. Quando o trabalho é executado, o supervisor opta por um novo líder e move a réplica primária para a instância do SQL Server do líder.

Depois de executar o trabalho, exclua-o. O objeto de trabalho no Kubernetes permanece após a conclusão, para que você possa exibir seu status. Você precisará excluir manualmente os trabalhos antigos depois de observar seu status. A exclusão de trabalho também exclui os logs do Kubernetes. Se você não excluir o trabalho, trabalhos de failover futuras falhará a menos que você altere o nome do trabalho e o seletor de pod. Para obter mais informações, consulte [trabalhos - executar até a conclusão](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

## <a name="rotate-credentials"></a>A rotação de credenciais

Gire as credenciais para atualizar o SA e a chave mestra.

Cópia de [creds.yaml girar](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script) usar localmente `kubectl` para aplicá-la ao seu cluster.

```azurecli
kubectl apply -f rotate-creds.yaml
```

## <a name="next-steps"></a>Próximas etapas

[Acessar o painel do Kubernetes com o serviço de Kubernetes do Azure (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)