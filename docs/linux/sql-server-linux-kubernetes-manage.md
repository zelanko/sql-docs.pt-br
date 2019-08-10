---
title: Gerenciar um grupo de disponibilidade Always On do SQL Server no Kubernetes
description: Este artigo explica como gerenciar um Grupo de Disponibilidade Always On do SQL Server no Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 893e502c35ae33ce6ff87efd88049db97a40f875
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952549"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Gerenciar grupo de disponibilidade Always On do SQL Server no Kubernetes

Para gerenciar o Grupos de Disponibilidade Always On no Kubernetes, crie um manifesto e aplique-o ao cluster. O manifesto é um arquivo `.yaml`.  

Os exemplos no artigo aplicam-se a todos os clusters do Kubernetes. Os cenários nesses exemplos são aplicados com relação a um cluster no Serviço de Kubernetes do Azure.

Confira um exemplo da implantação completa em [Implantar um Grupo de Disponibilidade Always On do SQL Server no cluster do Kubernetes](sql-server-linux-kubernetes-deploy.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Fazer failover – Grupo de disponibilidade do SQL Server no Kubernetes

Para fazer failover ou mover uma réplica primária para um nó diferente em um grupo de disponibilidade, conclua as seguintes etapas:

1. Definir um trabalho em um arquivo de manifesto.

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) – no repositório github [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) descreve um trabalho de failover.

  Copie o arquivo de manifesto para seu terminal de administração.

  Atualize o arquivo do seu ambiente.

  - Substitua `<containerName>` pelo nome do pod (por ex., mssql2-0) do destino do grupo de disponibilidade esperado.
  - Se o grupo de disponibilidade não estiver no namespace `ag1`, substitua `ag1` pelo namespace.

  Este arquivo define um trabalho de failover denominado `manual-failover`.

1. Para implantar o trabalho, use `kubectl apply`. O script a seguir implanta o trabalho.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  Após a implantação do trabalho, o Kubernetes, com o Operador do SQL Server, realiza as seguintes tarefas:
  
  - Rebaixa a réplica primária para secundária
  
  - Promove a réplica secundária para primária
  
  Após aplicar o arquivo de manifesto, o Kubernetes executa o trabalho. O trabalho faz o supervisor selecionar um novo líder e move a réplica primária para a instância do SQL Server do líder.

1. Verifique se o trabalho foi concluído.
  
  Depois que o Kubernetes executa o trabalho, é possível examinar o log.
  
  O exemplo a seguir retorna o status do trabalho denominado `manual-failover`.

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. Exclua o trabalho de failover manual. 

  >[!IMPORTANT]
  >É necessário excluir o trabalho manualmente antes de emitir outro failover manual.
  > 
  >O trabalho permanece no Kubernetes após a conclusão para você poder exibir seu status. É necessário excluir manualmente trabalhos antigos após anotar seu status. Excluir o trabalho também exclui os logs do Kubernetes. Se você não excluir o trabalho, futuros trabalhos de failover falharão, a menos que você altere o nome do trabalho e o seletor de pod. Para saber mais, confira [Trabalhos – Executar até a conclusão](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

  O comando a seguir exclui o trabalho.

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>Girar credenciais

Gire as credenciais para redefinir a senha da conta `sa` do SQL Server e a [chave mestra de serviço](../relational-databases/security/encryption/service-master-key.md) do SQL Server. 

Para concluir essa tarefa, você criará segredos no cluster do Kubernetes e um trabalho para girar as credenciais.

Antes de girar as credenciais, crie um segredo para a senha e a chave mestre.

O script a seguir cria um segredo chamado `new-sql-secrets`. Antes de executar o script, substitua `<>` pelas senhas complexas do `sapassword` e do `masterkeypassword`. Use senhas diferentes para cada respectivo valor.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

Conclua as etapas a seguir para cada instância do SQL Server que precisa da chave mestra ou da senha `sa`.

1. Copie [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) para seu terminal de administração.

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) no repositório github [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) é um exemplo de um manifesto para esse trabalho.

  Antes de aplicar esse manifesto, atualize o manifesto para seu ambiente. Examine e altere as seguintes configurações, conforme necessário.

  - Verifique o namespace. Atualize, se necessário. O exemplo a seguir em um manifesto aplica-se a um namespace chamado `ag1`.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - Verifique o nome da instância do SQL Server. Atualize, se necessário. O exemplo a seguir em uma especificação de manifesto aplica-se a uma instância do SQL Server chamada `mssql1`.

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  Salve o arquivo de manifesto atualizado em sua estação de trabalho.

1. Use `kubectl` para implantar o trabalho.

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  O Kubernetes atualiza a chave mestra e a senha `sa` para uma instância do SQL Server em um grupo de disponibilidade.

1. Verifique se o trabalho foi concluído. Execute o seguinte comando: Para verificar se o trabalho foi concluído, execute 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  Depois que o trabalho for bem sucedido, a chave mestra e a senha `sa` para uma instância do SQL Server serão atualizadas.


1. Antes de executar o trabalho novamente, exclua o trabalho. Cada nome de trabalho deve ser exclusivo.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

Para definir a mesma senha `sa` para todas as instâncias do SQL Server, repita as etapas acima para cada instância do SQL Server.

## <a name="next-steps"></a>Próximas etapas

[Acessar o painel do Kubernetes com o AKS (Serviço de Kubernetes do Azure)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
