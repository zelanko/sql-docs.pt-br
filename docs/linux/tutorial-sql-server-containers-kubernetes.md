---
title: "Configurar um contêiner do SQL Server no Kubernetes para alta disponibilidade | Microsoft Docs"
description: "Este tutorial mostra como implantar uma solução de alta disponibilidade do SQL Server com Kubernetes no serviço de contêiner do Azure."
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux,mvc
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: a21856b3a864373f84ad304484ecdd88ac17f52a
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="configure-a-sql-server-container-in-kubernetes-for-high-availability"></a>Configurar um contêiner do SQL Server no Kubernetes para alta disponibilidade

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Saiba como configurar uma instância do SQL Server em Kubernetes no serviço de contêiner do Azure (AKS), no armazenamento persistente para alta disponibilidade (HA). A solução fornece resiliência. Se a instância do SQL Server falhar, Kubernetes automaticamente recria em um novo pod. AKS fornece resiliência contra uma falha de nó Kubernetes. 

Este tutorial demonstra como configurar uma instância do SQL Server altamente disponível em contêineres que usam AKS. 

> [!div class="checklist"]
> * Criar uma senha de SA
> * Criar armazenamento
> * Criar a implantação
> * Conecte-se com o SQL Server Management Studio (SSMS)
> * Verifique se a falha e recuperação

## <a name="ha-solution-that-uses-kubernetes-running-in-azure-container-service"></a>HA solução que usa Kubernetes em execução no serviço de contêiner do Azure

Kubernetes 1.6 e posterior oferece suporte para [classes de armazenamento](http://kubernetes.io/docs/concepts/storage/storage-classes/), [volume persistente declarações](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)e o [tipo de volume de disco do Azure](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). Você pode criar e gerenciar suas instâncias do SQL Server nativamente no Kubernetes. O exemplo neste artigo mostra como criar um [implantação](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) para obter uma configuração de alta disponibilidade semelhante a uma instância de cluster de failover do disco compartilhado. Nessa configuração, Kubernetes desempenha a função do orchestrator cluster. Quando uma instância do SQL Server em um contêiner falha, o orchestrator inicializa outra instância do contêiner que é anexado ao mesmo armazenamento persistente.

![Diagrama do cluster Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

No diagrama anterior, `mssql-server` é um contêiner em uma [pod](http://kubernetes.io/docs/concepts/workloads/pods/pod/). Kubernetes organiza os recursos do cluster. Um [conjunto de réplicas](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) garante que o pod é automaticamente recuperado após uma falha de nó. Aplicativos se conectam ao serviço. Nesse caso, o serviço representa um balanceador de carga que hospeda um endereço IP que permanece o mesmo após a falha do `mssql-server`.

No diagrama a seguir, o `mssql-server` contêiner falhou. Como o orquestrador Kubernetes garante a contagem de correta de instâncias íntegras na réplica definida e inicia um novo contêiner de acordo com a configuração. O orchestrator inicia um nova pod no mesmo nó, e `mssql-server` reconecta-se ao mesmo armazenamento persistente. O serviço se conecta ao criado novamente `mssql-server`.

![Diagrama do cluster Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

No diagrama a seguir, o nó que hospeda o `mssql-server` contêiner falhou. O orchestrator inicia pod de novo em um nó diferente, e `mssql-server` reconecta-se ao mesmo armazenamento persistente. O serviço se conecta ao criado novamente `mssql-server`.

![Diagrama do cluster Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>Prerequisites

* **Cluster Kubernetes**
   - O tutorial exige um cluster Kubernetes. Usam as etapas [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) para gerenciar o cluster. 

   - Consulte [implantar um cluster do serviço de contêiner do Azure (AKS)](http://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster) para criar e conectar-se a um cluster de Kubernetes de nó único em AKS com `kubectl`. 

   >[!NOTE]
   >Para proteger contra falhas de nó, um cluster Kubernetes requer mais de um nó.

* **2.0.23 CLI do Azure**
   - As instruções neste tutorial foram validadas em relação a CLI do Azure 2.0.23.

## <a name="create-an-sa-password"></a>Criar uma senha de SA

Crie uma senha de SA no cluster Kubernetes. Kubernetes pode gerenciar as informações de configuração confidenciais, como senhas como [segredos](http://kubernetes.io/docs/concepts/configuration/secret/).

O comando a seguir cria uma senha para a conta SA:

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   Substituir `MyC0m9l&xP@ssw0rd` com uma senha complexa.

   Para criar um segredo no Kubernetes chamado `mssql` que contém o valor `MyC0m9l&xP@ssw0rd` para o `SA_PASSWORD`, execute o comando.


## <a name="create-storage"></a>Criar armazenamento

Configurar um [volume persistente](http://kubernetes.io/docs/concepts/storage/persistent-volumes/) e [volume persistente declaração](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) no cluster Kubernetes. Conclua as seguintes etapas: 

1. Criar um manifesto para definir a classe de armazenamento e o volume persistente declaração.  O manifesto especifica o provedor de armazenamento, parâmetros, e [recuperar política](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming). O cluster Kubernetes usa esse manifesto para criar o armazenamento persistente. 

   O exemplo a seguir yaml define uma classe de armazenamento e a declaração de volume persistente. O provedor de classe de armazenamento é `azure-disk`, pois este cluster Kubernetes é no Azure. O tipo de conta de armazenamento é `Standard_LRS`. A declaração de volume persistente é denominada `mssql-data`. Os metadados de declaração de volume persistentes incluem uma anotação conectando-o novamente para a classe de armazenamento. 

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

1. Crie a declaração de volume persistente Kubernetes.

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

   `<PersistentVolumeClaim>` é o nome da declaração do volume persistente.

   Na etapa anterior, a declaração de volume persistente é denominada `mssql-data`. Para ver os metadados sobre a declaração de volume persistente, execute o seguinte comando:

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   Os metadados retornados incluem um valor chamado `Volume`. Esse valor é mapeado para o nome do blob.

   ![Captura de tela de metadados retornados, incluindo o Volume](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   O valor para o volume corresponde a parte do nome do blob na imagem a seguir do portal do Azure: 

   ![Nome do portal de blob de captura de tela do Azure](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. Verifique se o volume persistente.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` retorna metadados sobre o volume persistente que foi criado e associado à declaração de volume persistente automaticamente. 

## <a name="create-the-deployment"></a>Criar a implantação

Neste exemplo, o contêiner que hospeda a instância do SQL Server é descrito como um objeto de implantação Kubernetes. A implantação cria um conjunto de réplicas. O conjunto de réplicas cria o pod. 

Nesta etapa, crie um manifesto para descrever o contêiner com base no SQL Server [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) imagem do Docker. O manifesto referencia o `mssql-server` volume persistente de declaração e o `mssql` segredo que já foram aplicados ao cluster Kubernetes. O manifesto também descreve uma [service](http://kubernetes.io/docs/concepts/services-networking/service/). Esse serviço é um balanceador de carga. O balanceador de carga garante que o endereço IP persista após a instância do SQL Server é recuperada. 

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
           image: microsoft/mssql-server-linux
           ports:
           - containerPort: 1433
           env:
           - name: ACCEPT_EULA
             value: "Y"
           - name: SA_PASSWORD
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

   Copie o código anterior em um novo arquivo, chamado `sqldeployment.yaml`. Atualize os seguintes valores: 

   * `value: "Developer"`: Define o contêiner para executar o SQL Server Developer edition. Edição de desenvolvedor não está licenciada para dados de produção. Se a implantação é para uso em produção, defina a edição apropriada (`Enterprise`, `Standard`, ou `Express`). 

      >[!NOTE]
      >Para obter mais informações, consulte [a licença do SQL Server](http://www.microsoft.com/sql-server/sql-server-2017-pricing).

   * `persistentVolumeClaim`: Esse valor requer uma entrada para `claimName:` que mapeia para o nome usado para a declaração de volume persistente. Este tutorial usa `mssql-data`. 

   * `name: SA_PASSWORD`: Define a imagem de contêiner para definir a senha de SA, conforme definido nesta seção.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     Quando Kubernetes implanta o contêiner, ele se refere ao segredo denominado `mssql` para obter o valor da senha. 

   >[!NOTE]
   >Usando o `LoadBalancer` tipo de serviço, a instância do SQL Server é acessível remotamente (por meio da internet) na porta 1433.

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

   Na imagem acima, o pod tem um status de `Running`. Este status indica que o contêiner está pronto. Isso pode levar vários minutos.

   >[!NOTE]
   >Após a implantação é criada, pode levar alguns minutos antes do pod está visível. O atraso é porque o cluster extrai o [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) imagem do Docker hub. Depois que a imagem é colocada na primeira vez, implantações subsequentes podem ser mais rápidas se a implantação é para um nó que já tem a imagem em cache nele. 

1. Verifique se que os serviços estão em execução. Execute o seguinte comando:

   ```azurecli
   kubectl get services 
   ```

   Esse comando retorna os serviços em execução, bem como os endereços IP internos e externos para os serviços. Anote o endereço IP externo para o `mssql-deployment` service. Use esse endereço IP para se conectar ao SQL Server. 

   ![Captura de tela de comando de serviço get](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Para obter mais informações sobre o status dos objetos no cluster Kubernetes, execute:

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>Conecte-se à instância do SQL Server

Se você configurou o contêiner conforme descrito, você pode se conectar com um aplicativo de fora da rede virtual do Azure. Use o `sa` conta e o externo de endereços IP para o serviço. Use a senha que você configurou como o segredo Kubernetes. 

Você pode usar os seguintes aplicativos para se conectar à instância do SQL Server. 

* [SSMS](http://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssms)

* [SSDT](http://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   Para conectar-se com `sqlcmd`, execute o seguinte comando:

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   Substitua os seguintes valores:
      
    - `<External IP Address>` com o endereço IP para o `mssql-deployment` serviço 
    - `MyC0m9l&xP@ssw0rd` com sua senha

## <a name="verify-failure-and-recovery"></a>Verifique se a falha e recuperação

Para verificar a falha e recuperação, você pode excluir o pod. Siga as etapas a seguir:

1. Lista o pod executando o SQL Server.

   ```azurecli
   kubectl get pods
   ```

   Observe o nome do pod de executando o SQL Server.

1. Exclua o pod.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` o valor é retornado da etapa anterior para nome pod. 

Kubernetes automaticamente recria pod para recuperar uma instância do SQL Server e conectar-se para o armazenamento persistente. Use `kubectl get pods` para verificar se um novo pod é implantado. Use `kubectl get services` para verificar se o endereço IP para o novo contêiner é o mesmo. 

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu como implantar contêineres do SQL Server em um cluster de Kubernetes para alta disponibilidade. 

> [!div class="checklist"]
> * Criar uma senha de SA
> * Criar armazenamento
> * Criar a implantação
> * Conecte-se com o SQL Server Management estúdios (SSMS)
> * Verifique se a falha e recuperação

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
>[Introdução ao Kubernetes](http://docs.microsoft.com/en-us/azure/aks/intro-kubernetes)


