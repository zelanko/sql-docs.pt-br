---
title: Implantar um grupo de disponibilidade Always On do SQL Server em um cluster Kubernetes
description: Este artigo explica os parâmetros para os Kubernetes Always On do SQL Server grupo operador globais requisitos de disponibilidade
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 07d0929dbdf60c31f1518a19a2999f0845d7d2e2
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713122"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>Implantar um grupo de disponibilidade Always On do SQL Server em um cluster Kubernetes

O exemplo neste artigo implanta um grupo de disponibilidade Always On do SQL Server em um cluster Kubernetes com três réplicas. As réplicas secundárias estão no modo de confirmação síncrona.

No Kubernetes, a implantação inclui um operador do SQL Server, os contêineres do SQL Server e carga dos serviços de Balanceador. O operador orquestra o grupo de disponibilidade automaticamente. Este artigo explica como:

- Implante o operador, contêineres do SQL Server e serviços de balanceamento de carga.
- Conecte-se ao grupo de disponibilidade com os serviços.
- Adicione um banco de dados para o grupo de disponibilidade.

## <a name="requirements"></a>Requisitos

- Um cluster AKS Kubernetes com a versão mais recente
- Pelo menos três nós
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- Acesso a [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) repositório do GitHub

> [!NOTE]
> Você pode usar qualquer tipo de cluster do Kubernetes. Para criar um cluster Kubernetes no serviço de Kubernetes do Azure (AKS), consulte [criar um cluster AKS](https://docs.microsoft.com/azure/aks/create-cluster).
>
> Use a versão mais recente do Kubernetes. A versão específica depende de sua assinatura e região. Ver [versões de suporte para o Kubernetes no AKS](https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions).  
>
> O script a seguir cria um cluster de quatro nós do Kubernetes no Azure. Antes de executar a substituição do script `<latest version>` com a versão mais recente disponível. Por exemplo, `1.12.5`.
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>Implantar o operador, contêineres do SQL Server e serviços de balanceamento de carga

1. Criar uma [namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/).

      Este exemplo usa um namespace chamado `ag1`. Execute o seguinte comando para criar o namespace.
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      Todos os objetos que pertencem a essa solução estão no `ag1` namespace.

1. Configure e implante o manifesto do operador do SQL Server.

      Copie o SQL Server [ `operator.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) do arquivo do [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      O `operator.yaml` arquivo é o manifesto de implantação para o operador de Kubernetes.
    
      Aplique o manifesto para o cluster Kubernetes.
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. Criar um segredo do Kubernetes com senhas para o `sa` conta e a chave mestra da instância do SQL Server.

      Criar o segredo com `kubectl`.
      
      O exemplo a seguir cria um segredo chamado `sql-secrets` no `ag1` namespace. O segredo armazena duas senhas:
      
      - `sapassword` armazena a senha para o SQL Server `sa` conta.
      - `masterkeypassword` armazena a senha usada para criar a chave mestre do SQL Server. 
    
   Copie o script para o seu terminal. Substitua cada `<>` com uma senha complexa e execute o script para criar o segredo.
    
   >[!NOTE]
   >A senha não é possível usar `&` ou `` ` `` caracteres.
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. Implante o recurso personalizado do SQL Server.

      Copie o manifesto do SQL Server [ `sqlserver.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) partir [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      >[!NOTE]
      >O `sqlserver.yaml` arquivo descreve contêineres do SQL Server, declarações de volume persistente, volumes persistentes e serviços de balanceamento de carga que são necessários para cada instância do SQL Server.
    
      Aplique o manifesto para o cluster Kubernetes.
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
A imagem a seguir mostra um aplicativo com êxito de `kubectl apply` para este exemplo.

![Criar sqlservers](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

Depois de aplicar o manifesto do SQL Server, o operador implanta os contêineres do SQL Server.

Kubernetes coloca os contêineres em pods. Use `kubectl get pods --namespace ag1` para ver o status dos pods. A imagem a seguir mostra o exemplo de implantação depois que os pods do SQL Server são implantados. 

![criado pods](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>Monitore a implantação

Você pode usar o [painel do Kubernetes com o serviço de Kubernetes do Azure](https://docs.microsoft.com/azure/aks/kubernetes-dashboard) para monitorar a implantação.

Use `az aks browse` para iniciar o painel. 

## <a name="connect-to-the-availability-group-with-the-services"></a>Conectar-se ao grupo de disponibilidade com os serviços

O [ `ag-services.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) partir [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) exemplo descreve os serviços de balanceamento de carga que podem se conectar a réplicas de grupo de disponibilidade. 

- `ag1-primary` Fornece um ponto de extremidade para se conectar à réplica primária.
- `ag1-secondary` Fornece um ponto de extremidade para se conectar a qualquer réplica secundária.

Quando você aplica o arquivo de manifesto, o Kubernetes cria os serviços de balanceamento de carga para cada tipo de réplica. O serviço de balanceamento de carga inclui um endereço IP. Use esse endereço IP para conectar-se ao tipo de réplica que você precisa.

Para implantar os serviços, execute o comando a seguir.

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

Depois de implantar os serviços, use `kubectl get services --namespace ag1` para identificar o endereço IP para os serviços.

Com o endereço IP, você pode se conectar à instância do SQL Server que hospeda cada tipo de réplica.

Mostra a imagem a seguir:

- A saída do `kubectl get services` para o namespace `ag1`.

- Os serviços de balanceamento de carga que são criados para cada contêiner do SQL Server. Use esses endereços IP como pontos de extremidade para se conectar diretamente às instâncias do SQL Server no cluster.

- O `sqlcmd` conexão à réplica primária, com o `sa` conta por meio do ponto de extremidade do balanceador de carga.

![Conectar](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>Adicionar um banco de dados ao grupo de disponibilidade

>[!NOTE]
>Neste momento, o SQL Server Management Studio não é possível adicionar um banco de dados para um grupo de disponibilidade. Usar o Transact-SQL.

Depois que o Kubernetes cria os contêineres do SQL Server, conclua as seguintes etapas para adicionar um banco de dados para o grupo de disponibilidade.

1. [Conectar-se](sql-server-linux-kubernetes-connect.md) para uma instância do SQL Server no cluster.

1. Criar um banco de dados.

      ```sql
      CREATE DATABASE [demodb]
      ```

1. Faça um backup completo do banco de dados para iniciar a cadeia de log.

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. Adicione o banco de dados para o grupo de disponibilidade.

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
O grupo de disponibilidade é criado com a propagação automática para que o SQL Server cria automaticamente as réplicas secundárias.

Você pode exibir o estado do grupo de disponibilidade do painel grupos de disponibilidade do SQL Server Management Studio.

![painel](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>Próximas etapas

- [Conectar-se a um grupo de disponibilidade do SQL Server em um cluster Kubernetes](sql-server-linux-kubernetes-connect.md)

- [Gerenciar um grupo de disponibilidade do SQL Server em um cluster Kubernetes](sql-server-linux-kubernetes-manage.md)

- [SQL Server dá suporte a grupos de disponibilidade em contêineres em um cluster Kubernetes](sql-server-ag-kubernetes.md)
