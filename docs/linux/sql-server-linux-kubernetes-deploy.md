---
title: Implantar o SQL Server sempre no grupo de disponibilidade no Cluster Kubernetes
description: Este artigo explica os parâmetros para os Kubernetes Always On do SQL Server grupo operador globais requisitos de disponibilidade
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4d24cd2ab59e1a7959f5a8ac1c929ff2e5e8e54a
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049596"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-kubernetes-cluster"></a>Implantar um SQL Server sempre no grupo de disponibilidade no Cluster Kubernetes

## <a name="requirements"></a>Requisitos

- Um cluster Kubernetes
- Kubernetes versão 1.11.0 ou superior
- Quatro ou mais nós
- [kubectl](http://kubernetes.io/docs/tasks/tools/install-kubectl/).

  >[!NOTE]
  >Você pode usar qualquer tipo de cluster do Kubernetes. Para criar um cluster Kubernetes no serviço de Kubernetes do Azure (AKS), consulte [criar um cluster AKS](http://docs.microsoft.com/azure/aks/create-cluster.md).
  > O script a seguir cria um cluster de quatro nós do Kubernetes no Azure.
  >```azure-cli
  az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version 1.11.1
  >```

## <a name="steps"></a>Etapas

1. Configurar o armazenamento

  Em ambientes de nuvem, como o Azure, configure [volumes persistentes](http://kubernetes.io/docs/concepts/storage/persistent-volumes/) para cada instância do SQL Server.

  Para criar volumes persistentes no Azure, consulte `pv.yaml` e `pvc.yaml` na [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates).

  Para criar o armazenamento, execute o seguinte comando:

  ```azurecli
  kubectl apply -f <pv.yaml>
  ```

1. Crie os segredos do Kubernetes para a senha de SA e a chave mestra.

  O exemplo a seguir cria dois segredos. `sapassword` é a senha de SA e `masterkeypassword` destina-se a chave mestra. Antes de executar esse script substitua `<MyC0mp13xP@55w04d!>` com outra senha complexa para cada segredo.

   ```azurecli
   kubectl create secret generic sql-secrets --from-literal='sapassword=<MyC0mp13xP@55w04d!>' --from-literal='masterkeypassword=<MyC0mp13xP@55w04d!>'
   ```

1. Configure e implante o manifesto do operador do SQL Server.

  Copie o operador do SQL Server `operator.yaml` do arquivo do [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

  O `operator.yaml` arquivo é o manifiest de implantação para o operador de Kubernetes.

  Para configurar o manifesto, atualize o `operator.yaml` arquivo para o seu ambiente.

  Aplique o manifesto para o cluster Kubernetes.

  ```azurecli
  kubectl apply -f operator.yaml
  ```

1. Implante o recurso personalizado do SQL Server.

  Copie o manifesto do SQL Server `sqlserver.yaml` partir [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

  Aplique o manifesto para o cluster Kubernetes.

  ```azurecli
  kubectl apply -f sqlserver.yaml
  ```

Depois de implantar o manifesto do SQL Server, o operador implanta instâncias do SQL Server como pods em contêineres.

Depois que o script for concluído, o operador de Kubernetes criará o armazenamento, as instâncias do SQL Server, os serviços do balanceador de carga. Você pode monitorar a implantação com [painel do Kubernetes](http://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Depois que o Kubernetes cria os contêineres do SQL Server conclua as seguintes etapas para adicionar um banco de dados para o grupo de disponibilidade:

1. [Conectar-se](sql-server-linux-kubernetes-connect.md) para uma instância do SQL Server no cluster.

1. Criar um banco de dados.

1. Faça um backup completo do banco de dados para iniciar a cadeia de log.

1. Adicione o banco de dados para o grupo de disponibilidade.

O grupo de disponibilidade é criado com a propagação automática para que o SQL Server criará automaticamente as réplicas secundárias.

## <a name="next-steps"></a>Próximas etapas

[Conectar-se ao grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-linux-kubernetes-connect.md)

[Gerenciar grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-linux-kubernetes-manage.md)

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)