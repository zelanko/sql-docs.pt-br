---
title: Gerenciar um grupo de disponibilidade SQL Server Always On Kubernetes
description: Este artigo explica como gerenciar um SQL Server sempre no grupo de disponibilidade no Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 808f49ff5060ba6a6ffe9e864cfc2710fe6251e6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705531"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Gerenciar o SQL Server Always On Kubernetes do grupo de disponibilidade

Para gerenciar um grupo de disponibilidade AlwaysOn no Kubernetes, crie um manifesto e aplicá-lo ao cluster. O manifesto é um `.yaml` arquivo.  

Os exemplos neste artigo se aplicam a todos os cluster de Kubernetes. Os cenários nesses exemplos são aplicados em relação a um cluster no serviço Kubernetes do Azure.

Veja um exemplo da implantação completa no [implantar um SQL Server sempre no grupo de disponibilidade no Kubernetes Cluster](sql-server-linux-kubernetes-deploy.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Failover - grupo de disponibilidade do SQL Server no Kubernetes

Para fazer failover ou mover uma réplica primária para um nó diferente em um grupo de disponibilidade, conclua as seguintes etapas:

1. Defina um trabalho em um arquivo de manifesto.

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) -na [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) repositório github descreve um trabalho de failover.

  Copie o arquivo de manifesto para seu terminal de administração.

  Atualize o arquivo para o seu ambiente.

  - Substitua `<containerName>` com o nome do pod do destino do grupo de disponibilidade esperada (por exemplo, mssql2-0).
  - Se o grupo de disponibilidade não está no `ag1` namespace, substitua `ag1` com o namespace.

  Esse arquivo define um trabalho de failover denominado `manual-failover`.

1. Para implantar o trabalho, use `kubectl apply`. O script a seguir implanta o trabalho.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  Depois que o trabalho for implantado, o kubernetes com o operador do SQL Server, realiza as seguintes tarefas:
  
  - Rebaixa a réplica primária para secundária
  
  - Promove a réplica especificada para o primário
  
  Depois de aplicar o arquivo de manifesto, o Kubernetes executa o trabalho. O trabalho faz com que o supervisor selecione um novo líder e move a réplica primária para a instância do SQL Server do líder.

1. Verifique se que o trabalho for concluído.
  
  Depois que o Kubernetes é executado o trabalho, você pode examinar o log.
  
  O exemplo a seguir retorna o status do trabalho nomeado `manual-failover`.

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. Exclua o trabalho de failover manual. 

  >[!IMPORTANT]
  >Você deve excluir manualmente o trabalho antes de emitir outro failover manual.
  > 
  >O objeto de trabalho no Kubernetes permanece após a conclusão, para que você possa exibir seu status. Você precisará excluir manualmente os trabalhos antigos depois de observar seu status. A exclusão de trabalho também exclui os logs do Kubernetes. Se você não excluir o trabalho, trabalhos de failover futuras falhará a menos que você altere o nome do trabalho e o seletor de pod. Para obter mais informações, consulte [trabalhos - executar até a conclusão](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

  O comando a seguir exclui o trabalho.

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>A rotação de credenciais

Girar as credenciais para redefinir a senha para o SQL Server `sa` conta e o SQL Server [chave mestra de serviço](../relational-databases/security/encryption/service-master-key.md). 

Para concluir essa tarefa, você criará novos segredos no cluster Kubernetes e, em seguida, criar um trabalho para girar as credenciais.

Antes de girar as credenciais, faça um novo segredo para a senha e a chave mestra.

O script a seguir cria um segredo chamado `new-sql-secrets`. Antes de executar o script, substitua `<>` com senhas complexas para o `sapassword` e o `masterkeypassword`. Use senhas diferentes para cada respectivo valor.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

Conclua as seguintes etapas para cada instância do SQL Server que precisa da chave mestra ou `sa` senha.

1. Cópia [ `rotate-creds.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) para a administração do terminal.

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) no [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) repositório do github é um exemplo de um manifesto para esse trabalho.

  Antes de aplicar esse manifesto, atualize o manifesto para o seu ambiente. Revisar e alterar as configurações a seguir, conforme necessário.

  - Verifique se o namespace. Atualize se necessário. O exemplo a seguir em um manifesto aplica-se a um namespace chamado `ag1`.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - Verifique se o nome da instância do SQL Server. Atualize se necessário. O exemplo a seguir em uma especificação de manifesto se aplica a uma instância do SQL Server denominada `mssql1`.

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  Salve o arquivo de manifesto atualizado para sua estação de trabalho.

1. Use `kubectl` para implantar o trabalho.

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes atualiza a chave mestra e `sa` senha para uma instância do SQL Server em um grupo de disponibilidade.

1. Verifique se que o trabalho for concluído. Execute o seguinte comando: Para verificar se o trabalho for concluído, execute 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  Depois que o trabalho for bem-sucedido, a chave mestra e `sa` senha para uma instância do SQL Server são atualizados.


1. Antes de executar o trabalho novamente, exclua o trabalho. Cada nome de trabalho deve ser exclusivo.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

Para definir o mesmo `sa` senha para todas as instâncias do SQL Server, repita as etapas acima para cada instância do SQL Server.

## <a name="next-steps"></a>Próximas etapas

[Acessar o painel do Kubernetes com o serviço de Kubernetes do Azure (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
