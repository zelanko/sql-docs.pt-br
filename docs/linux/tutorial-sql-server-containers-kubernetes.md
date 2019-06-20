---
title: Implantar um contêiner do SQL Server em Kubernetes com serviços de Kubernetes do Azure (AKS) | Microsoft Docs
description: Este tutorial mostra como implantar uma solução de alta disponibilidade do SQL Server com o Kubernetes no serviço Kubernetes do Azure.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: mvc
ms.technology: linux
ms.openlocfilehash: 236ae198b77f8fdc63a6c4d5069e3b335a44a472
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704844"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>Implantar um contêiner do SQL Server em Kubernetes com serviços de Kubernetes do Azure (AKS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Saiba como configurar uma instância do SQL Server em Kubernetes no serviço de Kubernetes do Azure (AKS), com o armazenamento persistente de alta disponibilidade (HA). A solução fornece resiliência. Se a instância do SQL Server falhar, Kubernetes automaticamente recria em um pod de novo. Kubernetes também fornece resiliência contra uma falha de nó.

Este tutorial demonstra como configurar uma instância do SQL Server altamente disponível em um contêiner no AKS. Você também pode criar [grupos de disponibilidade Always On para contêineres do SQL Server](sql-server-ag-kubernetes.md). Para comparar as duas soluções diferentes de Kubernetes, consulte [alta disponibilidade para contêineres do SQL Server](sql-server-linux-container-ha-overview.md).

> [!div class="checklist"]
> * Criar uma senha de SA
> * Criar armazenamento
> * Criar a implantação
> * Conecte-se com o SQL Server Management Studio (SSMS)
> * Verifique se a falha e recuperação

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>Solução de HA no Kubernetes em execução no serviço Kubernetes do Azure

Kubernetes 1.6 ou posterior tem suporte para [classes de armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/), [declarações de volume persistente](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)e o [tipo de volume de disco do Azure](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). Você pode criar e gerenciar suas instâncias do SQL Server nativamente no Kubernetes. O exemplo neste artigo mostra como criar uma [implantação](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) para atingir uma configuração de alta disponibilidade semelhante a uma instância de cluster de failover de disco compartilhado. Nessa configuração, o Kubernetes desempenha a função de orquestrador de cluster. Quando uma instância do SQL Server em um contêiner de falha, o orquestrador inicializa a outra instância do contêiner que anexa ao mesmo armazenamento persistente.

![Diagrama de cluster do Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

No diagrama anterior, `mssql-server` é um contêiner em um [pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/). O Kubernetes orquestra os recursos do cluster. Um [conjunto de réplicas](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) garante que o pod é automaticamente recuperado após uma falha de nó. Aplicativos se conectam ao serviço. Nesse caso, o serviço representa um balanceador de carga que hospeda um endereço IP que permanece o mesmo após a falha do `mssql-server`.

No diagrama a seguir, o `mssql-server` contêiner falhou. Como o orquestrador Kubernetes garante a contagem correta de instâncias íntegras na réplica definida e inicia um novo contêiner de acordo com a configuração. O orquestrador inicia um pod de novo no mesmo nó, e `mssql-server` reconecta-se ao mesmo armazenamento persistente. O serviço se conecta ao criada novamente `mssql-server`.

![Diagrama de cluster do Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

No diagrama a seguir, o nó que hospeda o `mssql-server` contêiner falhou. O orquestrador inicia o pod de novo em um nó diferente, e `mssql-server` reconecta-se ao mesmo armazenamento persistente. O serviço se conecta ao criada novamente `mssql-server`.

![Diagrama de cluster do Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>Prerequisites

* **Cluster do Kubernetes**
   - O tutorial requer um cluster Kubernetes. Usam as etapas [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) para gerenciar o cluster. 

   - Ver [implantar um cluster do serviço de contêiner do Azure (AKS)](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster) para criar e conectar-se a um cluster do Kubernetes de nó único no AKS com `kubectl`. 

   >[!NOTE]
   >Para proteger contra falhas de nó, um cluster Kubernetes requer mais de um nó.

* **CLI do Azure 2.0.23**
   - As instruções neste tutorial foram validadas em relação a CLI do Azure 2.0.23.

## <a name="create-an-sa-password"></a>Criar uma senha de SA

Crie uma senha de SA no cluster Kubernetes. Kubernetes podem gerenciar as informações de configuração confidenciais, como senhas, como [segredos](https://kubernetes.io/docs/concepts/configuration/secret/).

O comando a seguir cria uma senha para a conta SA:

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   Substitua `MyC0m9l&xP@ssw0rd` com uma senha complexa.

   Para criar um segredo no Kubernetes chamado `mssql` que contém o valor `MyC0m9l&xP@ssw0rd` para o `SA_PASSWORD`, execute o comando.


## <a name="create-storage"></a>Criar armazenamento

Configurar uma [volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) e [declaração de volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) no cluster Kubernetes. Conclua as seguintes etapas: 

1. Criar um manifesto para definir a classe de armazenamento e o volume persistente declaração.  O manifesto especifica o provedor de armazenamento, parâmetros, e [recuperar política](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming). O cluster Kubernetes usa esse manifesto para criar o armazenamento persistente. 

   O exemplo a seguir yaml define uma classe de armazenamento e a declaração de volume persistente. O provedor de classe de armazenamento é `azure-disk`, porque não é esse cluster Kubernetes no Azure. O tipo de conta de armazenamento é `Standard_LRS`. A declaração de volume persistente é denominada `mssql-data`. Os metadados de declaração de volume persistente incluem uma anotação, conectando-o novamente para a classe de armazenamento. 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   Salve o arquivo (por exemplo, **pvc.yaml**).

1. Crie a declaração de volume persistente no Kubernetes.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` é o local onde você salvou o arquivo.

   O volume persistente é automaticamente criado como uma conta de armazenamento do Azure e associado à declaração de volume persistente. 

    ![Captura de tela do comando de declaração de volume persistente](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. Verifique se a declaração de volume persistente.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` é o nome da declaração de volume persistente.

   Na etapa anterior, a declaração de volume persistente é denominada `mssql-data`. Para ver os metadados sobre a declaração de volume persistente, execute o seguinte comando:

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   Os metadados retornados incluem um valor chamado `Volume`. Esse valor é mapeado para o nome do blob.

   ![Captura de tela de metadados retornados, incluindo o Volume](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   O valor para o volume corresponde à parte do nome do blob na imagem a seguir do portal do Azure: 

   ![Nome do blob de portal de captura de tela do Azure](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. Verifique se o volume persistente.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` retorna metadados sobre o volume persistente que foi automaticamente criado e associado à declaração de volume persistente. 

## <a name="create-the-deployment"></a>Criar a implantação

Neste exemplo, o contêiner que hospeda a instância do SQL Server é descrito como um objeto de implantação do Kubernetes. A implantação cria um conjunto de réplicas. O conjunto de réplicas cria o pod. 

Nesta etapa, crie um manifesto para descrever o contêiner com base no SQL Server [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) imagem do Docker. As referências do manifestas a `mssql-server` declaração de volume persistente e o `mssql` segredo que já foram aplicados ao cluster Kubernetes. O manifesto também descreve uma [serviço](https://kubernetes.io/docs/concepts/services-networking/service/). Esse serviço é um balanceador de carga. O balanceador de carga garante que o endereço IP persista após a instância do SQL Server é recuperada. 

1. Crie um manifesto (um arquivo YAML) para descrever a implantação. O exemplo a seguir descreve uma implantação, incluindo um contêiner com base na imagem de contêiner do SQL Server.

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2017-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
           - name: ACCEPT_EULA
             value: "Y"
           - name: MSSQL_SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   Copie o código anterior para um novo arquivo, chamado `sqldeployment.yaml`. Atualize os valores a seguir: 

   * MSSQL_PID `value: "Developer"`: Define o contêiner para executar o SQL Server Developer edition. Edição de desenvolvedor não está licenciada para dados de produção. Se a implantação for para uso em produção, defina a edição apropriada (`Enterprise`, `Standard`, ou `Express`). 

      >[!NOTE]
      >Para obter mais informações, consulte [como licenciar o SQL Server](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

   * `persistentVolumeClaim`: Esse valor requer uma entrada para `claimName:` que mapeia para o nome usado para a declaração de volume persistente. Este tutorial usa `mssql-data`. 

   * `name: SA_PASSWORD`: Configura a imagem de contêiner para definir a senha de SA, conforme definido nesta seção.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     Quando o contêiner Kubernetes é implantado, ele se refere ao segredo chamado `mssql` para obter o valor da senha. 

   >[!NOTE]
   >Usando o `LoadBalancer` tipo de serviço, a instância do SQL Server está acessível remotamente (por meio da internet) na porta 1433.

   Salve o arquivo (por exemplo, **sqldeployment.yaml**).

1. Crie a implantação.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` é o local onde você salvou o arquivo.

   ![Captura de tela do comando de implantação](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   A implantação e o serviço são criados. Instância do SQL Server está em um contêiner, conectado ao armazenamento persistente.

   Para exibir o status do pod, digite `kubectl get pod`.

   ![Captura de tela do comando de pod get](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   Na imagem anterior, o pod tem um status de `Running`. Este status indica que o contêiner está pronto. Isso pode levar vários minutos.

   >[!NOTE]
   >Depois que a implantação é criada, ele pode levar alguns minutos antes do pod está visível. O atraso é porque o cluster efetua pull de [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) imagem do Docker hub. Depois que a imagem é colocada na primeira vez, as implantações subsequentes podem ser mais rápidas se a implantação for para um nó que já tem a imagem em cache ali. 

1. Verifique se que os serviços estão em execução. Execute o seguinte comando:

   ```azurecli
   kubectl get services 
   ```

   Esse comando retorna os serviços em execução, bem como os endereços IP internos e externos para os serviços. Anote o endereço IP externo para o `mssql-deployment` service. Use esse endereço IP para se conectar ao SQL Server. 

   ![Captura de tela do comando de serviço de get](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Para obter mais informações sobre o status dos objetos no cluster Kubernetes, execute:

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>Conectar-se à instância do SQL Server

Se você tiver configurado o contêiner conforme descrito, você pode se conectar com um aplicativo de fora da rede virtual do Azure. Use o `sa` conta e o externo de endereços IP para o serviço. Use a senha que você configurou como o segredo do Kubernetes. 

Você pode usar os seguintes aplicativos para se conectar à instância do SQL Server. 

* [SSMS](https://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   Para conectar-se com `sqlcmd`, execute o seguinte comando:

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   Substitua os valores a seguir:
      
    - `<External IP Address>` com o endereço IP para o `mssql-deployment` serviço 
    - `MyC0m9l&xP@ssw0rd` com sua senha

## <a name="verify-failure-and-recovery"></a>Verifique se a falha e recuperação

Para verificar a falha e recuperação, você pode excluir o pod. Siga as etapas a seguir:

1. Liste o pod executando o SQL Server.

   ```azurecli
   kubectl get pods
   ```

   Anote o nome do pod executando o SQL Server.

1. Exclua o pod.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` é o valor retornado da etapa anterior para o nome do pod. 

Kubernetes automaticamente recria o pod para recuperar uma instância do SQL Server e conectar-se para o armazenamento persistente. Use `kubectl get pods` para verificar se um novo pod é implantado. Use `kubectl get services` para verificar se o endereço IP para o novo contêiner é o mesmo. 

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu como implantar contêineres do SQL Server para um cluster Kubernetes para alta disponibilidade. 

> [!div class="checklist"]
> * Criar uma senha de SA
> * Criar armazenamento
> * Criar a implantação
> * Conecte-se com o SQL Server Management Studio (SSMS)
> * Verifique se a falha e recuperação

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
>[Introdução ao Kubernetes](https://docs.microsoft.com/azure/aks/intro-kubernetes)


