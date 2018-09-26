---
title: Configurar um grupo de disponibilidade Always On do SQL Server em contêineres do Docker no Kubernetes | Microsoft Docs
description: Este tutorial mostra como implantar um SQL Server sempre no grupo de disponibilidade com o Kubernetes no serviço de contêiner do Azure.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: tutorial
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux,mvc
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6d21866f3f7004dff1ea86ca4f608580a79ab754
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049352"
---
# <a name="configure-a-sql-server-always-on-availability-group-on-docker-containers-in-kubernetes-with-azure-kubernetes-service-aks"></a>Configurar um grupo de disponibilidade Always On do SQL Server em contêineres do Docker no Kubernetes com o serviço de Kubernetes do Azure (AKS)

Este tutorial demonstra como configurar uma instância do SQL Server altamente disponível em um contêiner no AKS. Você também pode [implantar um contêiner do SQL Server em Kubernetes](tutorial-sql-server-containers-kubernetes.md). Para comparar as duas soluções diferentes de Kubernetes, consulte [alta disponibilidade para contêineres do SQL Server](sql-server-linux-container-ha-overview.md).

Neste tutorial, você aprenderá como:  

> [!div class="checklist"]
> * Criar armazenamento
> * Implantar o operador do SQL Server em um cluster do Kubernetes 
> * Crie os segredos do Kubernetes
> * Implantar agentes de integridade e de instâncias do SQL Server
> * Conectar-se à réplica primária
> * Adicionar um banco de dados ao grupo de disponibilidade

Este tutorial demonstra a arquitetura [serviço de Kubernetes do Azure (AKS)](http://docs.microsoft.com/azure/aks/). Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Este diagrama representa a solução que você pode fazer neste tutorial:

![cluster do kubernetes-ag](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

### <a name="deployment-methodology-for-kubernetes"></a>Metodologia de implantação para o Kubernetes

Várias das etapas neste artigo criar um manifesto e, em seguida, implante o manifesto para o cluster. O manifesto é um arquivo YAML com a descrição dos objetos Kubernetes que você implanta.

Os arquivos YAML neste exemplo estão disponíveis em [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability).

Os objetos incluem armazenamento, operadores, pods, contêineres e serviços.

## <a name="prerequisites"></a>Prerequisites

* Familiaridade geral com essas tecnologias

  * [Kubernetes](http://kubernetes.io) versão 1.8
  * [Serviço de Kubernetes do Azure (AKS)](http://docs.microsoft.com/azure/aks/)
  * [SQL Server no Docker](quickstart-install-connect-docker.md)
  * [Grupo de disponibilidade do SQL Server Always On](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

* Um cluster Kubernetes com quatro nós.

  Para obter instruções, consulte [Tutorial: implantar um cluster do serviço de Kubernetes do Azure (AKS)](http://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster).

* Instale [ `kubectl` ](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#install-the-kubectl-cli).

## <a name="configuration-and-deployment-procedures"></a>Procedimentos de implantação e configuração

O tutorial mostra como aplicar os arquivos YAML ao cluster Kubernetes.

## <a name="create-the-secrets"></a>Crie os segredos

Para criar os segredos do Kubernetes para armazenar as senhas para a conta SA do SQL Server e a chave mestre do SQL Server, execute o comando a seguir.

```azurecli
kubectl create secret generic sql-secrets --from-literal=sapassword="MyC0m9l&xP@ssw0rd" --from-literal=masterkeypassword="MyC0m9l&xP@ssw0rd2"
```

Em um ambiente de produção, use uma senha diferente e complexa.

## <a name="deploy-the-operator"></a>Implantar o operador

Um operador de Kubernetes implanta instâncias do SQL Server e configura o grupo de disponibilidade no cluster Kubernetes. 

Consulte um operador de exemplo no [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml)

Baixe `operator.yaml` de [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/)

Implante o operador como uma réplica de implantação do Kubernetes.

Para implantar o operador:

Implantar o operador com o `kubectl apply` comando.

```azurecli
kubectl apply -f operator.yaml
```

## <a name="create-the-sql-server-ag-deployment"></a>Criar a implantação do grupo de disponibilidade do SQL Server

A próxima etapa cria instâncias do SQL Server e o grupo de disponibilidade em uma implantação de Kubernetes. Depois de aplicar essa implantação para o cluster, o operador será implantar instâncias do SQL Server como contêineres do Docker. Essa implantação resultará em três StatefulSets com um pod. Cada pod incluirá dois contêineres:

* Instância do SQL Server com base no `mssql-server` imagem
* Supervisor de alta disponibilidade

Além disso, a implantação descreve um serviço de Balanceador de carga para o ouvinte do grupo de disponibilidade

Para implantar o mssql-server:

1. Cópia [sqlserver.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) em seu computador.
2. Atualização `sqlserver.yaml` para o seu ambiente.


Para implantar as instâncias do SQL Server e criar o grupo de disponibilidade, execute o comando a seguir.

```azurecli
kubectl apply -f sqlserver.yaml
```

## <a name="deploy-ag-services"></a>Serviços de implantação de grupo de disponibilidade

O cluster Kubernetes cria serviços de Balanceador de carga para chamadas diretas para as réplicas no grupo de disponibilidade.

[AG services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) cria quatro serviços.

* AG1 primário conecta-se à réplica primária.
* sincronização de secundário AG1 se conecta a uma réplica secundária síncrona.
* AG1-secundário-async se conecta a uma réplica secundária assíncrona.
* AG1-secundário-config se conecta a uma réplica somente de configuração. 

  >[!NOTE]
  >Esses serviços de Balanceador de carga são fornecidos como exemplos. Neste tutorial não há réplica somente de configuração.


Implante os serviços do balanceador de carga para que você pode se conectar ao grupo de disponibilidade.

Para implantar os serviços, execute o comando a seguir.

```azurecli
kubectl apply -f ag-services.yaml
```

### <a name="monitor-the-deployment"></a>Monitore a implantação

Você pode usar [painel do Kubernetes com o serviço de Kubernetes do Azure (AKS)](https://docs.microsoft.com/en-us/azure/aks/kubernetes-dashboard) para monitorar a implantação. 

Use `az aks browse` para iniciar o painel. 

Após a implantação, apenas AG associação lista e pós-inicialização script T-SQL pode ser atualizado. Outras propriedades não podem ser atualizadas - o recurso deve ser excluído e recriado. As credenciais para os usuários gerada automaticamente podem ser girados usando um `mssql-server-k8s-rotate-creds` trabalho.

## <a name="connect-to-the-sql-server-instance-hosting-the-primary-replica"></a>Conectar-se à instância do SQL Server que hospeda a réplica primária

O `ag-services.yaml` descreve um nome de serviço do Kubernetes `ag1-primary`. `ag1-primary` cria um balanceador de carga do Azure que apontar a instância do SQL Server que hospeda a réplica primária. Use o endereço IP externo do serviço como servidor de destino `sa` assim como da conta e a senha que você criou anteriormente no `mssql secret` a senha.

Use `kubectl get services` para obter esse endereço IP.

Por exemplo:

![Obter um exemplo de serviço](media\tutorial-sql-server-ag-containers-kubernetes\KubernetesGetServices.png)

Na imagem acima, `ag1-primary` serviço tem um endereço IP externo do `104.42-50.138`. 

Para se conectar ao SQL Server com a autenticação do SQL, use o `sa` conta, o valor de `sapassword` do segredo que você criou e esse endereço IP.

Por exemplo:

```cmd
sqlcmd -S 104.42.50.138 -U sa -P "MyC0m9l&xP@ssw0rd"
```

![Conectar-se com o sqlcmd](./media/tutorial-sql-server-ag-containers-kubernetes/sqlcmdConnect.png)

Você também pode se conectar com [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md).

Para verificar sua conexão, a instância do SQL Server que hospeda a réplica primária, execute a consulta a seguir:

```sql
SELECT @@SERVERNAME;
```

A consulta retorna o nome da instância do SQL Server que hospeda a réplica primária.

Neste ponto, o cluster Kubernetes tem três instâncias do SQL Server em contêineres do docker. Um grupo de disponibilidade abrange todas as três instâncias do SQL Server, mas nenhum banco de dados está no grupo de disponibilidade. A próxima etapa é adicionar um banco de dados para o grupo de disponibilidade.

## <a name="add-a-database-to-the-availability-group"></a>Adicionar um banco de dados ao grupo de disponibilidade

Para adicionar um banco de dados para o grupo de disponibilidade:

1. Criar um banco de dados

  ```sql
  CREATE DATABASE [DemoDB]
  ```

1. Faça um backup do banco de dados para iniciar a cadeia de log de transações completo

  ```sql
  BACKUP DATABASE [DemoDB] 
  TO  DISK = N'/var/opt/mssql/data/DemoDB.bak' 
    WITH NOFORMAT, 
    NOINIT,  
    NAME = N'DemoDB-Full Database Backup', 
    SKIP, 
    NOREWIND, 
    NOUNLOAD,  
    STATS = 10;
  GO
  ```

1. Adicionar o banco de dados para o grupo de disponibilidade

  ```sql
  ALTER AVAILABILITY GROUP ag1 ADD DATABASE [DemoDB]; 
  ```

A réplica é configurada automaticamente com o modo de propagação automática para que o grupo de disponibilidade propaga o banco de dados em réplicas secundárias.

No SQL Server Management Studio, você pode se conectar à réplica primária e ver o grupo de disponibilidade no painel.

O exemplo a seguir mostra o grupo de disponibilidade com réplicas em três nós configurados no painel de controle.

![Painel do AG1](./media/tutorial-sql-server-ag-containers-kubernetes/ssms_AG1.png)

## <a name="verify-failure-and-recovery"></a>Verifique se a falha e recuperação

Para verificar se o failover e detecção de falha, você pode excluir o pod hospedando a réplica primária. Kubernetes será optam por uma nova réplica primária e redirecione o ouvinte. Em seguida, ele recriará o pod excluído. 

Para demonstrar esse processo, execute as seguintes etapas:

1. Liste o pod executando o SQL Server.

   ```azurecli
   kubectl get pods
   ```

2. Identifique o pod executando a réplica primária.

   A se conectar à réplica primária usando o IP e a consulta externa `@@servername` ou use `kubectl` para obter o pod apropriado. Esse comando retornará o nome do pod que inclui o contêiner em execução a réplica primária do AG:

   ```azurecli
   kubectl get pods --selector="role.ag.mssql.microsoft.com/ag1"="primary" --output=jsonpath={.items..metadata.name}
   ```

3. Exclua o pod.

   ```azurecli
   kubectl delete pod <podName>
   ```

Substitua `<podName>` com o valor retornado da etapa anterior para o nome do pod. 

Kubernetes automaticamente realiza failover em uma das réplicas secundárias de sincronização disponíveis, bem como recria o pod excluído.

## <a name="clean-up-resources"></a>Limpar recursos

Quando não for mais necessário, exclua o grupo de recursos e todos os recursos relacionados. Execute o seguinte comando:
>[!WARNING]
>Esse comando exclui completamente tudo no grupo de recursos. Nenhum dos componentes do cluster do Kubernetes estará disponível depois de excluir o grupo de recursos.

```azurecli
az group delete --name <MyResourceGroup>
```

Para executar o comando acima, substitua `<MyResourceGroup>` com o nome do seu grupo de recursos. 

Azure exclui o grupo de recursos.

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu como:  

> [!div class="checklist"]
> * Criar armazenamento
> * Implantar o operador do SQL Server em um cluster do Kubernetes 
> * Crie os segredos do Kubernetes
> * Implantar agentes de integridade e de instâncias do SQL Server
> * Conectar-se à réplica primária
> * Adicionar um banco de dados ao grupo de disponibilidade

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
>[Introdução ao Kubernetes](http://docs.microsoft.com/azure/aks/intro-kubernetes)
>[gerenciar o SQL Server em Kubernetes](sql-server-linux-kubernetes-manage.md)