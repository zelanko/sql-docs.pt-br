---
title: Implantar um grupo de disponibilidade do SQL Server Always On em um cluster do Kubernetes
description: Este artigo explica os parâmetros para os requisitos globais do operador de grupo de disponibilidade do SQL Server Kubernetes Always On
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1e8825336edd4e55812f6037bbb4479a3b225e3f
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028736"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>Implantar um grupo de disponibilidade do SQL Server Always On em um cluster do Kubernetes

O exemplo neste artigo implanta um grupo de disponibilidade SQL Server Always On em um cluster do Kubernetes com três réplicas. As réplicas secundárias estão no modo de confirmação síncrona.

No Kubernetes, a implantação inclui um operador de SQL Server, os contêineres de SQL Server e os serviços de balanceador de carga. O operador orquestra o grupo de disponibilidade automaticamente. Este artigo explica como:

- Implantar o operador, os contêineres de SQL Server e os serviços de balanceamento de carga.
- Conectar-se ao grupo de disponibilidade com os serviços.
- Adicionar um banco de dados ao grupo de disponibilidade.

## <a name="requirements"></a>Requisitos

- Um cluster do AKS Kubernetes com a versão mais recente
- Pelo menos três nós
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- Acesso ao repositório GitHub [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)

> [!NOTE]
> Você pode usar qualquer tipo de cluster do Kubernetes. Para criar um cluster do Kubernetes no AKS (Serviço de Kubernetes do Azure), confira [Criar um cluster no AKS](https://docs.microsoft.com/azure/aks/create-cluster).
>
> Use a versão mais recente do Kubernetes. A versão específica depende de sua assinatura e região. Confira [Versões compatíveis do Kubernetes no AKS](https://docs.microsoft.com/azure/aks/supported-kubernetes-versions).  
>
> O script a seguir cria um cluster do Kubernetes de quatro nós no Azure. Antes de executar o script, substitua `<latest version>` pela versão mais recente disponível. Por exemplo, `1.12.5`.
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>Implantar o operador, os contêineres de SQL Server e os serviços de balanceamento de carga

1. Crie um [namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/).

      Este exemplo usa um namespace chamado `ag1`. Execute o seguinte comando para criar o namespace.
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      Todos os objetos que pertencem a essa solução estão no namespace `ag1`.

1. Configurar e implantar o manifesto do operador de SQL Server.

      Copie o arquivo [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) do SQL Server de [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      O arquivo `operator.yaml` é o manifesto de implantação para o operador do Kubernetes.
    
      Aplique o manifesto ao cluster do Kubernetes.
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. Crie um segredo para o Kubernetes com senhas para a conta `sa` e a chave mestra de instância do SQL Server.

      Crie o segredo com `kubectl`.
      
      O exemplo a seguir cria um segredo chamado `sql-secrets` no namespace `ag1`. O segredo armazena duas senhas:
      
      - `sapassword` armazena a senha da conta `sa` do SQL Server.
      - `masterkeypassword` armazena a senha usada para criar a chave mestra do SQL Server. 
    
   Copie o script para o terminal. Substitua cada `<>` por uma senha complexa e execute o script para criar o segredo.
    
   >[!NOTE]
   >A senha não pode usar caracteres `&` nem `` ` ``.
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. Implante o recurso personalizado do SQL Server.

      Copie o manifesto [`sqlserver.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) do SQL Server de [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      >[!NOTE]
      >O arquivo `sqlserver.yaml` descreve os contêineres do SQL Server, as declarações de volume persistentes, os volumes persistentes e os serviços de balanceamento de carga necessários para cada instância do SQL Server.
    
      Aplique o manifesto ao cluster do Kubernetes.
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
A imagem a seguir mostra a aplicação bem-sucedida de `kubectl apply` para este exemplo.

![Criar sqlservers](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

Depois de aplicar o manifesto do SQL Server, o operador implanta os contêineres do SQL Server.

O Kubernetes coloca os contêineres em pods. Use `kubectl get pods --namespace ag1` para ver o status dos pods. A imagem a seguir mostra o exemplo de implantação depois que os pods do SQL Server são implantados. 

![Pods criados](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>Monitorar a implantação

Você pode usar o [painel do Kubernetes com o Serviço de Kubernetes do Azure](https://docs.microsoft.com/azure/aks/kubernetes-dashboard) para monitorar a implantação.

Use `az aks browse` para iniciar o painel. 

## <a name="connect-to-the-availability-group-with-the-services"></a>Conectar-se ao grupo de disponibilidade com os serviços

O [`ag-services.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) do exemplo [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) descreve os serviços de balanceamento de carga que podem se conectar a réplicas do grupo de disponibilidade. 

- `ag1-primary` fornece um ponto de extremidade para conectar-se à réplica primária.
- `ag1-secondary` fornece um ponto de extremidade para conectar-se a qualquer réplica secundária.

Quando você aplica o arquivo de manifesto, o Kubernetes cria os serviços de balanceamento de carga para cada tipo de réplica. O serviço de balanceamento de carga inclui um endereço IP. Use esse endereço IP para se conectar ao tipo de réplica de que você precisa.

Para implantar os serviços, execute o comando a seguir.

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

Depois de implantar os serviços, use `kubectl get services --namespace ag1` para identificar o endereço IP dos serviços.

Com o endereço IP, você pode se conectar à instância do SQL Server que hospeda cada tipo de réplica.

A imagem a seguir mostra:

- A saída de `kubectl get services` para o namespace `ag1`.

- Os serviços de balanceamento de carga que são criados para cada contêiner do SQL Server. Use esses endereços IP como pontos de extremidade para se conectar diretamente às instâncias do SQL Server no cluster.

- A conexão `sqlcmd` com a réplica primária, com a conta `sa` por meio do ponto de extremidade do balanceador de carga.

![Conectar](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>Adicionar um banco de dados ao grupo de disponibilidade

>[!NOTE]
>Neste momento, o SQL Server Management Studio não pode adicionar um banco de dados a um grupo de disponibilidade. Use Transact-SQL.

Depois que o Kubernetes criar os contêineres do SQL Server, conclua as etapas a seguir para adicionar um banco de dados ao grupo de disponibilidade.

1. [Conecte-se](sql-server-linux-kubernetes-connect.md) a uma instância do SQL Server no cluster.

1. Criar um banco de dados.

      ```sql
      CREATE DATABASE [demodb]
      ```

1. Faça um backup completo do banco de dados para iniciar a cadeia de logs.

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. Adicione um banco de dados ao grupo de disponibilidade.

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
O grupo de disponibilidade é criado com propagação automática, de modo que o SQL Server cria automaticamente as réplicas secundárias.

Você pode exibir o estado do grupo de disponibilidade no painel de grupos de disponibilidade do SQL Server Management Studio.

![painel](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>Próximas etapas

- [Conectar-se com um grupo de disponibilidade do SQL Server em um cluster do Kubernetes](sql-server-linux-kubernetes-connect.md)

- [Gerenciar um grupo de disponibilidade do SQL Server em um cluster do Kubernetes](sql-server-linux-kubernetes-manage.md)

- [O SQL Server dá suporte a grupos de disponibilidade em contêineres em um cluster do Kubernetes](sql-server-ag-kubernetes.md)
